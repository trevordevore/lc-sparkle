# lc-sparkle
LiveCode Builder wrapper around [Sparkle](https://sparkle-project.org)

## Setting up Sparkle

Please refer to the [Sparkle documentation](https://sparkle-project.org/documentation/) to familiarize yourself with the various requirements. You are intersted in everything starting with the security section. Here is a direct link:

https://sparkle-project.org/documentation/#3-segue-for-security-concerns

## Using Sparkle in your application

Once you have configured your Info.plist file with the `SUFeedURL` key you can use Sparkle to update your application. 

According to the Sparkle documentation, the second time your application is launched Sparkle will ask the user if they want to check for updates. If they do then `sparkleGetAutomaticallyChecksForUpdates()` will return true. You can create a preference UI for this setting and call `sparkleSetAutomaticallyChecksForUpdates()` to update the setting.

### Confirm that the feel url is set up correctly

```
put sparkleGetFeedUrl()
```

### Check for updates from a "Check For Updates" menu item

```
sparkleCheckForUpdates()
```

## Check for updates silently in the background

This checks for updates in the background but will display UI to the user if an update is found.

```
sparkleCheckForUpdatesInBackground()
```

## Check for updates silently in background but don't alert user

This approach will only send callbacks. No UI is shown to the user.

```
sparkleCheckForUpdateInformation()
```

## SUAppcastItem Structure

Some of the callbacks include a parameter that is an array representing an SUAppcastItem object. It is referred to as an pAppcastItemArray. The array has the following keys:

- `title`
- `date`
- `description`
- `release notes url`
- `dsa signature`
- `minimum system version`
- `maximum system version`
- `file url`
- `version`
- `os`
- `display version`
- `info url`
- `content length`

## Callbacks

- `sparkleFinishedLoadingAppcast pAppcastItemsArray`: pAppcastItemsArray is a numerically indexed array of pAppcastItemArray arrays contained in the Appcast.
- `sparkleFoundUpdate pAppcastItemArray`
- `sparkleDidNotFindUpdate`
- `sparkleWillInstallUpdate pAppcastItemArray`
- `sparkleWillRelaunchApplication`
- `sparkleWillShowModalAlert`
- `sparkleDidShowModalAlert`
- `sparkleDownloadCanceledByUser`
- `sparkleWillInstallUpdateOnQuit pAppcastItemArray`
- `sparkelDidCancelInstallUpdateOnQuit pAppcastItemArray`
- `sparkleDidAbortWithError pErrorArray`: pErrorArray contains `description` and `failure reason` keys. You can display the `description` key to users.
