# 1. instance property 이용

```swift
import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
    }
    @IBAction func moveToDetail(_ sender: Any) {
        let detailVC = DetailViewController(nibName: "DetailViewController", bundle: nil)
	
				detailVC.someString = "test";        

        self.present(detailVC, animated: true, completion: nil)
    }
}

class DetailViewController: UIViewController {
    
    var someString = ""

    @IBOutlet weak var someLabel: UILabel!
    
    override func viewDidLoad() {
        super.viewDidLoad()

        someLabel.text = someString
    }
}
```

- `viewDidLoad()`가 실행되어야 `@IBOutlet` 같은 요소들이 메모리에 올라갈 준비가 된다.
- 인스턴스화된 Controller의 `viewDidLoad()`는  `.present()` 에 의해 실행되는데, 실행 이전에 그 Controller의 `@IBOutlet`에 접근하려 하면 error 발생
- `@IBOutlet` 같은 값은 외부에서 값을 할당하지 않는 것이 안전하기 때문에, Controller 내부의 property를 선언하여 값을 할당함. 이러한 방식을 통해 `viewDidLoad()` 의 실행 전에도 값을 할당할 수 있음.

# 2. segue

- 여러개의 view controller가 하나의 storyboard에 있을 때 주로 사용

```swift
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        if segue.identifier == "segueDetail" {
            if let detailVC = segue.destination as? SegueDetailViewController {
                detailVC.dataString = "abcd"
            }
        }
    }
```
