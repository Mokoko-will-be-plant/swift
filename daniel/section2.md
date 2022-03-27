# Passing Data

## PassingData_1

- instance property (parameter와 비슷)

```swift
    class ViewController: UIViewController {

        override func viewDidLoad() {
            super.viewDidLoad()
        }

        @IBAction func moveToDetail(_ sender: Any) {
            let detailVC = DetailViewController(nibName: "DetailViewController", bundle: nil)

            detailVC.someLabel.text = "aaa" // ** Crash
            detailVC.someString = "aaa 스트링"
            self.present(detailVC, animated: true, completion: nil)
            detailVC.someLabel.text = "aaa" // ** Possible

        }
    }

    class DetailViewController: UIViewController {

        var someString = ""

        // someString은 언제든지 인스턴스가 생성되면 사용 가능
        // But, IBOutlet은 viewDidLoad 라이프 사이클 이후에 사용 가능! 그전이면 크래시가 된다.
        @IBOutlet weak var someLabel: UILabel!

        override func viewDidLoad() {
            super.viewDidLoad()

            someLabel.text = someString
        }


    }

```

## PassingData_2

- segue

```swift
    override func prepare(for seque: UIStoryboardSeque, sender: Any?){
        if seque.identifier == "sequeDetail" {
            if let detailVC = seque.destination as? SequeDetailViewController {
                detailVC.dataString = "abcd"
            }
        }
    }
```

> PassingData_1, PassingData_2 취향 차이

## PassingData_3

- instance 직접접근 (양방향 바인딩 가능) ( 자식 > 부모 )

```swift

    // 해당 부분으로 instance 자체를 넘겨서, 받는 쪽에서 선언 후, 직접 접근
    @IBAction func moveToInstance(_ sender: Any){
        let detailVC = InstanceDetailViewController(nibName: "InstanceDetailViewController", bundle: nil)

        detailVC.mainVC = self

        self.present(detailVC, animted: true, completion: nil)
    }

    var mainVC: ViewController?
    @IBAction func sendDataMainVc(_ sender: Any){
        mainVC.datLabel.text = "some data"
        self.dismiss(animated: true, completion: nil)
    }
```

## PassingData_4

- delegate (delegation) pattern 대리 위임 대신 ( 자식 > 부모 )

```swift
    // Send
    @IBAction func moveToDelegage(_ sender: Any) {
         let detailVC = DelegateDetailViewControllerDelegate(nibName: "DelegateDetailViewControllerDelegate", bundle: nil)

        // 위에 인스턴스는 모든 것을 넘겨주는데에 비해, 해당 protocol 방식은 아래 Extension되는 부분만 넘겨줄 수 있도록 되어 있음!
        detailVC.delegate = self

        self.present(detailVC, animted: true, completion: nil)
    }

    // important!!!
    extension ViewController: DelegateDetailViewControllerDelegate {
        func passString(string: String) {
            self.dataLabel.text = string
        }
    }

    // Receive
    protocol DelegateDetailViewControllerDelegate: AnyObject {
        func passString(string: String)
    }

    class DelegateDetailViewController: UIViewController {
        weak var delegate: DelegateDetailViewControllerDelegate?

        @IBAction func passDataToMainVC(_ sender: Any) {
            delegate?.passString(string: "delegate pass Data")
        }
    }

```

## PassingData_5

```swift

```

## PassingData_6

```swift

```
