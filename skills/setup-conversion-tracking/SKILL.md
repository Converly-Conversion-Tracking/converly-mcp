---
name: setup-conversion-tracking
description: Set up Converly conversion tracking end to end. Use when the user wants to track form submissions as conversions, send leads to an ad platform like Google Ads, Meta or Google Analytics, or set up Converly for the first time.
---

# Set up conversion tracking with Converly

Tracking only works when THREE things are all true. A flow is published, the destination platform is connected (for server side platforms), and the Converly snippet is installed on the website. Never end this workflow without all three handled or handed to the user.

## Steps

1. **Understand the goal.** Ask which form tool the site uses (Typeform, Webflow forms, Gravity Forms and so on) and which ad platform conversions should go to, unless the user already said.

2. **Check the destination.** Call `list_destinations`. If the target platform isn't connected and it is a server side platform (its entry in `list_destination_types` has a non empty `connection_types`), call `connect_destination`. Share the link it returns, explain the account owner must open it in their browser and authorize, and ask them to tell you when they've finished. Then confirm with `check_handoff_status`. Browser side pixel platforms (empty `connection_types`) need no connection step.

3. **Build the flow.** Call `list_trigger_types` for the trigger id and `list_action_types` for the exact action config the destination needs. Create with `create_flow`, then run `validate_flow` and fix any problems it reports.

4. **Publish.** Call `publish_flow`. Read its result carefully. If `install_status.detection` is "never_seen", the loader has never phoned home from the site. That usually means the snippet still needs to be installed, so offer it. The check is quick to settle: the loader phones home when a page loads, so once the snippet is in, ask the user to open any page of their site and check `get_install_status` again. Detection flips to "confirmed" within moments. If it stays "never_seen" after a page load, the snippet is not live yet (site builders need a republish). Two setups never send the phone-home signal: sites using the Converly Webflow app, and visitors with privacy signals or unconsented cookie banners. For those, a real form submission appearing in `list_events` is the proof instead.

5. **Get the snippet installed.** Call `get_install_snippet` and give the user the script tag. Tell them to add it to their site's head section, or through their website platform's custom code setting. This step needs the user to act. Do not skip it and do not suggest testing before it is done.

6. **Verify.** Once the snippet is in place, ask the user to open any page of their site, then check `get_install_status`. "confirmed" proves the loader is running (and `origin_authorized: false` means the site domain is wrong, fix it with `update_site`). Then suggest a real form submission and check `list_events` for the captured conversion and `get_event_detail` for the per destination delivery result. Only the submission proves the form itself gets detected. `send_test_event` can fire a test conversion to a connected destination without a form submission.

## Cautions

- If a write is refused for billing, the account has no active trial or subscription. Tell the user to sort out their subscription in Converly, then continue.
- Never guess ids. Sites, flows, destinations and events all come from the list tools with prefixed ids.
