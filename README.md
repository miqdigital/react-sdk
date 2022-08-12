# ConfigCat SDK for React applications (alpha version)

https://configcat.com

ConfigCat SDK for React provides easy integration for your web application to ConfigCat.

## About

Manage features and change your software configuration using <a href="https://configcat.com" target="_blank">ConfigCat feature flags</a>
, without the need to re-deploy code. A <a href="https://app.configcat.com" target="_blank">10 minute trainable Dashboard</a>
allows even non-technical team members to manage features directly. Deploy anytime, release when confident.
Target a specific group of users first with new ideas. Supports A/B/n testing and soft launching.

ConfigCat is a <a href="https://configcat.com" target="_blank">hosted feature flag service</a>. Manage feature toggles across frontend, backend, mobile, desktop apps. <a href="https://configcat.com" target="_blank">Alternative to LaunchDarkly</a>. Management app + feature flag SDKs.

## Getting Started

The ConfigCat React SDK uses the Context API (requires React **16.3** or later) and Hook API (requires React **16.8** or later) to provide a better integration in your React application.

### 1. Install package:

_via NPM [package](https://npmjs.com/package/configcat-react):_

```PowerShell
npm i configcat-react
```

### 2. Go to the <a href="https://app.configcat.com/sdkkey" target="_blank">ConfigCat Dashboard</a> to get your *SDK Key*:

![SDK-KEY](https://raw.githubusercontent.com/ConfigCat/js-sdk/master/media/readme02-3.png  "SDK-KEY")

### 3. Import and initialize ConfigCatProvider

In most cases you should wrap your root component with `ConfigCatProvider` to access ConfigCat features in child components with Context API.

```js
import React from "react";
import { ConfigCatProvider } from "configcat-react";

function App() {
  return (
    <ConfigCatProvider sdkKey="#YOUR_SDK_KEY#">
      {/* your application code */}
    </ConfigCatProvider>
  );
}

export default App;
```

### 4. Get your setting value:

The React hooks (`useFeatureFlag`) way:
```js
function ButtonComponent() {
  const isAwesomeFeatureEnabled = useFeatureFlag(
    "isawesomefeatureenabled",
    false
  );

  return (
    <button
      disabled={!isAwesomeFeatureEnabled}
      onClick={() => alert("ConfigCat <3 React")}
    >
      isAwesomeFeature
    </button>
  );
}
```

The React HOC (`WithConfigCatClientProps`) way:
```js
function ButtonComponent() {
  const isAwesomeFeatureEnabled = useFeatureFlag(
    "isawesomefeatureenabled",
    false
  );

  return (
    <button
      disabled={!isAwesomeFeatureEnabled}
      onClick={() => alert("ConfigCat <3 React")}
    >
      isAwesomeFeature
    </button>
  );
}
```

## Sample/Demo app
  - [React](https://github.com/configcat/react-sdk/tree/main/samples/react-sdk-sample)

## Polling Modes
The ConfigCat SDK supports 3 different polling mechanisms to acquire the setting values from ConfigCat. After latest setting values are downloaded, they are stored in the internal cache then all requests are served from there. Read more about Polling Modes and how to use them at [ConfigCat Docs](https://configcat.com/docs/sdk-reference/react/).

## Sensitive information handling

The frontend/mobile SDKs are running in your users' browsers/devices. The SDK is downloading a [config.json](https://configcat.com/docs/requests/) file from ConfigCat's CDN servers. The URL path for this config.json file contains your SDK key, so the SDK key and the content of your config.json file (feature flag keys, feature flag values, targeting rules, % rules) can be visible to your users. 
This SDK key is read-only, it only allows downloading your config.json file, but nobody can make any changes with it in your ConfigCat account.  
Suppose you don't want your SDK key or the content of your config.json file visible to your users. In that case, we recommend you use the SDK only in your backend applications and call a backend endpoint in your frontend/mobile application to evaluate the feature flags for a specific application customer.  
Also, we recommend using [sensitive targeting comparators](https://configcat.com/docs/advanced/targeting/#sensitive-text-comparators) in the targeting rules of those feature flags that are used in the frontend/mobile SDKs.

## Browser compatibility
This SDK should be compatible with all modern browsers.

The SDK is [tested](https://github.com/configcat/react-sdk/actions/workflows/react-ci.yml) against the following browsers:
- Chrome (stable, latest, beta)
- Chromium (64.0.3282.0, 72.0.3626.0, 80.0.3987.0)
- Firefox (latest, latest-beta, 84.0).

These tests are running on each pull request, before each deploy, and on a daily basis. 

## Need help?
https://configcat.com/support

## Contributing
Contributions are welcome. For more info please read the [Contribution Guideline](CONTRIBUTING.md).

## About ConfigCat
- [Official ConfigCat SDK's for other platforms](https://github.com/configcat)
- [Documentation](https://configcat.com/docs)
- [Blog](https://blog.configcat.com)
