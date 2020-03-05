# github-load-all-comments
A Tampermonkey script to automatically load all hidden comments on Github

When this script is enabled, the 'Load Hidden Comments' button is triggered immediately on page load.

To see this in action, visit https://github.com/rust-lang/rust/pull/65819. With this script enabled, the "Load Hidden Comments" button should disappear shortly after the page loads.

## Background

Github has a "feature" that hides a large fraction of the comments in
long issue/PR threads, requiring the user to click a "Show hidden" button to see them.

Not only can this cut off important parts of a
discussion, clicking the button only reveals some of the hidden
comments. To show the entire thread, a user must:

1. Search on the page for "show hidden"
2. Click the button
3. Wait several seconds for an AJAX request to complete and the page to update
4. Go back to step 1 to see if there are more hidden comments

This must be done every time the user nagivates to an issue/PR page.

## Implementation

This is based on https://github.com/sindresorhus/refined-github/pull/2625, adjusted to use plain JavaScript instead of TypeScript.

Currently, the implementation relies on an undocumented query parameter to force loading all comments at once.
This avoids the repeatedly trigger the 'Load Hidden Comments' button (incurring a round-trip delay with each click).

This could stop working at any time - however, the current method has worked for several methods without any problems.

Hopefully, GitHub either lets this continue to work, or provides a way to opt out of "hidden comments" entirely.
. 
