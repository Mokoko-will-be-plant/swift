# App Build Intro

## xcode의 기본 설정

- 실행 Command+R

## class의 기본 사용 스타일

- Main.storyboard와 Controller 연결

## UIViewController를 사용하는 이유

- present 등 화면 이동 등 상속받아야만 부모 클래스에 있는 함수들을 사용할 수 있음

```swift

    class ViewController: UIViewController {
        @IBOutlet weak var testButton: UIButton!

        @IBAction func doSomething(_ sender: Any) {
            testButton.backgroundColor = .orange

            let storyboard = UIStoryboard(name: "Main", bundle: nil)
            let detailVC = storyboard.instantiateViewController(identifier: "DetailVC") as DetailVC

            self.present(detailVC, animated: true, completion: nil)
        }
    }

    class DetailVC: UIViewController {
        // 화면에 나올 준비 됐을 때,
        override func viewDidLoad() {
            super.viewDidLoad()
        }

        // 화면에 나오기 직전,
        override func viewWillAppear(_ animated: Bool) {
            super.viewWillAppear(animated)
        }

        // 화면에 나오고 난 후,
        override func viewDidAppear(_ animated: Bool) {
            super.viewDidAppear(animated)
        }

        // 화면에 사라지기 직전,
        override func viewWillDisappear(_ animated: Bool) {
            super.viewDidAppear(animated)
        }

        // 화면에 사리지고 난 후,
        override func viewDidDisappear(_ animated: Bool) {
            super.viewDidAppear(animated)
        }
    }
```

## IBAction 개념

- 화면 버튼의 액션과 연결된 기능

## IBOutlet 개념

- 화면 어딘가 연결 될 수 있는 변수
