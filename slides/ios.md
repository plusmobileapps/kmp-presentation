#### iOS

```swift [2|8-11|14-16|18-20]
import UIKit
import SharedCode

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        DI.init().getRepository().getDankMemes(
            onSuccess: onDankMemesLoaded(response:), 
            onError: onDankMemesError(error:)
        )
    }

    func onDankMemesLoaded(response: [Post]) {
        // update your table view 
    }
    
    func onDankMemesError(error: Any) {
        //show error
    }

}
```