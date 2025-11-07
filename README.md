# WhopPayments

The `WhopPayments SDK` provides a simple way to integrate Whop's payouts functionality into your iOS application.

## Install

Add `WhopPayments` to your Swift Package Manager dependencies and pin it to the latest release.

```swift
dependencies: [
    .package(url: "https://github.com/whopio/whopsdk-payments-swift.git", exact: "0.0.4")
]
```

## Integration Example

```swift
import SwiftUI
import WhopPayments

class MyTokenProvider: WhopTokenProvider {
    /// return an access token fetched from your
    /// backend.
    ///
    /// called when `WhopPayoutsView` appears and
    /// before expiration (within 60 seconds).
    ///
    /// the SDK handles caching and retries with
    /// exponential backoff on failure.
    func getToken() async -> WhopTokenResponse {
        let token = await fetchAccessToken()
        return WhopTokenResponse(accessToken: token)
    }
}

@main
struct MyApp: App {
    let tokenProvider = MyTokenProvider()

    var body: some Scene {
        WindowGroup {
            WhopPayoutsView(
                tokenProvider,
                companyId: "company_id",
                ledgerAccountId: "ledger_account_id"
            )
        }
    }
}
```

## Requirements

- iOS 17.0+
- Xcode 16.4+
- Swift 5.10+