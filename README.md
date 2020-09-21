# CSS Sharing Bug

In LWC we can [share CSS style sheet betweeen components](https://developer.salesforce.com/docs/component-library/documentation/en/lwc/lwc.create_components_css_share).

This works fine and is demonstrated in our LWC Recipes sample app.
However, this fails when deploying components one by one.

## Expected

All components deploy and CSS sharing works.

## Actual

Component with reference to style sheet fails to deploy with `No MODULE named markup://c:cssLibrary found `.

## Repro

Running these commands exposes the bug:
```sh
sfdx force:source:deploy -p force-app/main/default/lwc/contactTile
sfdx force:source:deploy -p force-app/main/default/lwc/cssLibrary
sfdx force:source:deploy -p force-app/main/default/lwc/compositionBasics
```

Last command fails with:
```
No MODULE named markup://c:cssLibrary found : [markup://c:compositionBasics]
```

What's intersting is that a full deploy of the project works fine:
```sh
sfdx force:source:deploy -p force-app
```