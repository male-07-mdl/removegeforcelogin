# Remove mandatory Geforce Experience login

The original Github page by Moyster is gone and while you can still view it using Wayback machine, I decided to create a proper Github page because Wayback doesn't have the files archived themselves.

The original method still works fine as of v3.28.0.412 and most likely will work until the possible end of Geforce Experience.

Credits go to Moyster (and co-contributors Still34, tahubird, hugmouse).

# How to remove the login

Go to

```
C:\Program Files\NVIDIA Corporation\NVIDIA GeForce Experience\www\
```

to find app.js.

You can use https://beautifier.io/ to make it more readable, but there's a lot of text and in case beautifier is taking too long, you can skip it.

**Replace**

```
if (e.domains.list.indexOf(n) > -1) return !0
```

with

```
if (e.domains.list.indexOf(n) > -1) return y.handleLoggedIn(e), !0
```

**Replace**

```
}, b.isLeftPaneVisible = function() {
                return !("choose" === b.nvActiveAuthView)
}
```

with

```
}, b.isLeftPaneVisible = function() {
                return !("choose" === b.nvActiveAuthView)
}, b.handleLoggedIn({
                sessionToken: "dummySessionToken",
                userToken: "dummyUserToken",
                user: {
                    core: {
                        displayName: "Anonymous",
                        primaryEmailVerified: true
                    }
                }
            });
```

**Replace**

```
Q.isShareSupported = !1, Q.isShareButtonClicked = !1
```

with

```
Q.isShareSupported = !0, Q.isShareButtonClicked = !0
```

**Optionally** find

```
y.info("automatically resent verification email"), u.endActionAsync(r, "EMAIL_NOT_VERIFIED"), b.showEmailVerification(e)
```

and remove

```
b.showEmailVerification(e)
```

# Note
Variable names may change in different versions, but the procedure should be the same, just make sure to change variable names.

I am also including information from original page on how to block telemetry.

Open hosts file in

```
C:\Windows\System32\drivers\etc
```

and add either

```
0.0.0.0 telemetry.gfe.nvidia.com
0.0.0.0 gfe.nvidia.com
0.0.0.0 gfwsl.geforce.com
0.0.0.0 services.gfe.nvidia.com
0.0.0.0 accounts.nvgs.nvidia.com
0.0.0.0 accounts.nvgs.nvidia.cn
0.0.0.0 events.gfe.nvidia.com
0.0.0.0 img.nvidiagrid.net
0.0.0.0 images.nvidiagrid.net
0.0.0.0 images.nvidia.com
0.0.0.0 ls.dtrace.nvidia.com
0.0.0.0 ota.nvidia.com
0.0.0.0 ota-downloads.nvidia.com
0.0.0.0 rds-assets.nvidia.com
0.0.0.0 assets.nvidiagrid.net
0.0.0.0 nvidia.tt.omtrdc.net
0.0.0.0 api.commune.ly
0.0.0.0 login.nvgs.nvidia.com
0.0.0.0 login.nvgs.nvidia.cn
```

to block telemetry, driver, Geforce Experience updates

or

```
0.0.0.0 ls.dtrace.nvidia.com
0.0.0.0 telemetry.gfe.nvidia.com
0.0.0.0 accounts.nvgs.nvidia.com
0.0.0.0 accounts.nvgs.nvidia.cn
0.0.0.0 nvidia.tt.omtrdc.net
0.0.0.0 api.commune.ly
0.0.0.0 login.nvgs.nvidia.com
0.0.0.0 login.nvgs.nvidia.cn
```

to block just telemtry and keep updates.
