# Implementations

### Label

```swift
override func viewDidLoad() {
	super.viewDidLoad()

	// viewController의 view 객체 접근 가능
	// UIcolor.red 생략 가능 .red는 UIcolor리턴하고
	// .backgoundColor는 UIcolor를 받기 때문에 쉬위프트가 자동으로 인식
	view.backgroundColor = .red
	
	let label = UILabel()
	label.text = "hello"

	// 배치 및 크기 필요
	label.frame = CGRect()

	// viewController의 최상위가 view이므로 view에 할당
	view.addSubview(label)
}
```



### TextField

사용자에게 입력을 받을 수 있다. 현재 ViewController에서 TextField를 인지하기 위해 delegate를 사용하여 참조해주어야한다.

```swift
// : UITextFieldDelegate(프로토콜)
searchTextField.delegate = self
```

검색 버튼, 키보드 버튼에서 입력이 끝날때의 처리를 해야한다.

```swift
@IBAction func searchPressed(_ sender: UIButton) {
        searchTextField.endEditing(true)
    }
    
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        searchTextField.endEditing(true)
        return true
    }
    
    // 입력 끝내기 직전 -> 성공, 실패
    func textFieldShouldEndEditing(_ textField: UITextField) -> Bool {
        if searchTextField.text != "" {
            return true
        } else {
            searchTextField.placeholder = "Type something"
            return false
        }
    }
    
    // 입력 끝낸 직후
    func textFieldDidEndEditing(_ textField: UITextField) {
        searchTextField.text = ""
        searchTextField.placeholder = "Search"
    }
```



### URLsession

네트워킹 작업을 수행하는 오브젝트.

```swift
func performRequest(urlString: String) {
    
    // 1. Create a URL
    if let url = URL(string: urlString) {
        
        // 2. Create a URLsession
        let session = URLSession(configuration: .default)
        
        // 3. Give the session a task
        let task = session.dataTask(with: url, completionHandler: handle(data:response:error:))
        
        // 4. Start task
        task.resume()
    }
}
```



### CoreLocation

현재 사용하고 있는 기기에 접근하여 위치 정보 얻을 수 있다. 이 기능을 사용하기 위해서는 먼저 사용자의 접근 허가 승인을 필요로 한다. .Info파일에서 `Privacy - Location When In Use Usage Description` 키를 등록하여 용도에 대한 디스크립션을 추가할 수 있다.

```swift
import CoreLocation

let locationManager = CLLocationManager()

locationManager.requestWhenInUseAuthorization()

// 한번만 사용할 경우
locationManager.requestLocation()

// 계속 정보 모니터링
locationManager.startUpdatingLocation()
```



### UITableView

데이터를 리스트형태로 보여주는 오브젝트이다. 메일, 챗뷰로사용된다. 리스트형 데이터를 표현하는 UI 컴포넌트이다. 입력 컴포넌트와 마찬가지로 델리게이션으로 수행된다. 각각의 요소는 UITableCell로 구성되어 있다. 기본 스타일, 선택시 변경사항등을 지정하여 사용할 수 있다. 셀(아이템)의 갯수로 테이블을 정의하고 각 셀에 포함될 데이터를 가공하여 넣는다.

```swift
tableView.delegate = self
tableView.dataSource = self

// tableView가 처음 실행될 때 리스트에 보일 데이터 정보를 요청한다.
// 아래에 소스를 보면 열의 갯수와 각 셀에 담을 정보를 업데이트하여 리턴한다.
extension ChatViewController: UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return messages.count
    }

    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
       // Fetch a cell of the appropriate type.
       let cell = tableView.dequeueReusableCell(withIdentifier: K.cellIdentifier, for: indexPath)
       
       // indexPath : 현재 셀 인덱스 
       cell.textLabel!.text = messages[indexPath.row].body
       return cell
    }
}

// tableView가 인터랙션하는 방식을 구현하는 파트.
extension ChatViewController: UITableViewDelegate {
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        print(indexPath.row)
    }
}
```

{% hint style="info" %}
delegate = self 코드를 대체하는 방법이 있다. 해당 UI컴포넌트를 command + 드래그하여 노란색아이콘에 드랍한 다음, Delegate를 선택한다.
{% endhint %}



### Custom Design Of Cell

1. create cocoa touch class
2. class name for cell
3. pick sub class UITableViewCell
4. check xib file

```swift

// Xip - Nip
// 디자인 파일과 조작하는 영역

// nip 등록
tableView.register(UINib(nibName: K.cellNibName, bundle: nil), forCellReuseIdentifier: K.cellIdentifier)

// as! MessgeCell 직접만든 셀로 변경, 따라서 main에서 만든 tableViewCell은 삭제해도 된다.
// ReusableCell identifier 설정 -> ReusableCell
let cell = tableView.dequeueReusableCell(withIdentifier: K.cellIdentifier, for: indexPath) as! MessageCell
cell.label.text = messages[indexPath.row].body
```



![](../.gitbook/assets/Untitled.png)

1. UIview ( label, ImageView )
2. StackView(label, ImageView)
3. 스택뷰 Alignment Top , Spacing , Constraint 조정
4. Label Lines 0 , Constraint 조정



### UITableViewCell Option

{% hint style="info" %}
\[attribute] - \[Accessary]
{% endhint %}

```swift
if tableView.cellForRow(at: indexPath)?.accessoryType == .checkmark {
    tableView.cellForRow(at: indexPath)?.accessoryType = .none
} else {
    tableView.cellForRow(at: indexPath)?.accessoryType = .checkmark
}
```



### UITableViewController

기존에는 ViewController에서 사용하였기에 extention을 사용하여 : UITableViewDataSource, : UITableViewDelegate를 상속해야했지만 UITableViewController자체 클래스를 사용하면 확장할 필요 없이 바로 사용할 수 있다.



### Initial View Controller

{% hint style="info" %}
main.storyboard -> viewController - \[attribute] - \[check initial view]
{% endhint %}



### Navigation bar

Barbutton object를 네비게이션에 추가하여 사용 가능하다.

{% hint style="info" %}
\[EDITOR] - \[embed in] - \[navigation controller]
{% endhint %}

```swift
// 네비게이션 타이틀
title = "⚡️FlashChat"

// 백버튼 없애기
navigationItem.hidesBackButton = true

// 메인 화면으로 돌아가기
navigationController?.popToRootViewController(animated: true)
```



### Navigating viewController

1\. 현재 페이지(VC)에서 다른 페이지 띄우기

```swift
self.present(secondVC, animated:ture, completion: nil)
```

2\. .cocoatouch&#x20;

UIKit 뿐만 아니라 애플에서 만든 라이브러리를 사용할 수 있다. 이를 활용하여 멀티 페이지를 설정하고 세그웨이 및 네비게이팅할 수 있게 된다. 세그웨이는 스크린에 나타날 화면을 애니메이션하는 방법을 말한다.

디자인 된 View Controller를 클릭(노란색네모 클릭)하고 Tab(identify)에서 커스텀 클래스를 CoCoa파일로 만든 클래스를 연동한다.

```swift
// one page
self.performSegue(withIdentifier: "goToResult", sender: self)

// multi page
// mainController(cocoa페이지를 호출하는)
override func prepare() {
	if segue.identifier == "goToResult {

		// downcasting by as, 왜냐면 prepare를 호춣하면 기본적으로 UIController를 가져오는데
		// 이때 우리가 ResultViewController나 bmiValue가 있는지 모르기 때문
		let destinationVC = segue.destination as! ResultViewController
		destinationVC.bmiValue = "0.0"
}

// secondController(cocoa페이지에서)
// go back to previous page
self.dismiss(animated: true, completion: nil
```



### Search Bar

마찬가지로 delegate Protocol을 사용하여 구현한다.

```swift
extension TodoListViewController: UISearchBarDelegate {
    
    func searchBarSearchButtonClicked(_ searchBar: UISearchBar) {
        
        let request : NSFetchRequest<Item> = Item.fetchRequest()
        let predicate = NSPredicate(format: "title CONTAINS[cd] %@", searchBar.text!)
        request.sortDescriptors = [NSSortDescriptor(key: "title", ascending: true)]
        
        loadItems(with: request, predicate: predicate)
    }
    
    func searchBar(_ searchBar: UISearchBar, textDidChange searchText: String) {
        // Excute this block when searchBar's text changed.
        
        if searchBar.text?.count == 0 {
            loadItems()
            
            DispatchQueue.main.async {
                // Ask to main queue run this methods that restoration searchBar states. before getting data
                
                searchBar.resignFirstResponder()
            }
        }
    }
}
```



### Link Category to Items

릴레이션이 연관된 데이터를 각 페이지에서 볼 수 있게 구현한다.

1. 각각의 ViewController를 생성하고 Segue를 연결
   * Segue에는 이동할 페이지의 이름을 기입한다.
   * 각각의 ViewController에 class name를 연결한다.
   * 만약 TableViewController일 경우 reusableCell 이름도 기입한다.
2. Core Data 파일에 Entities와 Relations를 설정
   * Attribute, Type, Optional
   * Relationship, Destination, Inverse
3. CategoryViewTable의 구현사항은 페이지가 로드되는 순간 카테고리 리스트가 보이고 해당 카테고리를 클릭하면 해당 카테고리 정보를 Items 페이지로 넘겨준다.

```swift
import UIKit
import CoreData

class CategoryViewController: UITableViewController {

    **//  MARK: - Initial States -------------------------------------**    
		//  categories
		//  persistentContainer context from AppDeleate

    

    **//  MARK: - Initial Methods ------------------------------------**
    //  loadCategories
    

    
    **//  MARK: - Model Create Method --------------------------------**
    @IBAction func addButtonPressed(_ sender: UIBarButtonItem) {
				// Create Alert
				// Set Alert Action
    }
    
    
    
    **//  MARK: - TableView Datasource Methods -----------------------**
    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int { 
    }

    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    }
    
    
    
    **//  MARK: - TableView Delegate Methods -------------------------**
    override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
				// Change View
    }
    
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        // Excute just before Change View
				// Passing the required data to destinationVC
    }
    
    
    **//  MARK: - Data Manipulation Methods --------------------------**
    func loadCategories(with request: NSFetchRequest<Category> = Category.fetchRequest()) {
        // Fetch Categories
				// Reload TableView 
    }
    
    func saveCategory() {
        // Save Categories
				// Reload TableView 
    }
```



### Dark mode

시스템 컬러를 사용하면 운영체제가 지원하는 다크모드를 사용할 수 있다. 커스텀 컬러를 다크모드와 사용하기 위해서는 Assets에서 플러스 버튼을 눌러 Color Set을 지정하면 된다.



### Avoid of pixelate Background

Assets에서 x1 x2 x3이미지 변환하는 방법, 벡터 파일을 사용하는 방법이 있다. 백터 파일의 경우, Vector Resizing, Single scale이 되도록 옵션을 변경하면 하나의 파일로 모든 해상도를 커버할 수 있다.



### Scroll

indexPath 오브젝트로 현재 1번째 섹션에 있는 마지막 리스트 아이템 인덱스를 가져온다. 현제 테이블 뷰에 섹션이 하나 박에 없어서 0 으로 입력한다. 이 후 테이블 뷰 스크롤 메서드를 호출하는데 해당 인덱스로 이동하는데 애니메이션을 사용할지 말지에 대해 옵션을 기입한다.

```swift
let indexPath = IndexPath(row: self.messages.count - 1, section: 0)
self.tableView.scrollToRow(at: indexPath, at: .top, animated: false)
```



### Alert

```swift
@IBAction func addButtonPressed(_ sender: UIBarButtonItem) {
        
	// 서로다른 클로저에서 사용될 변수
        var textField = UITextField()
        
	// 얼럿 창
        let alert = UIAlertController(title: "Add new Today Item", message: "", preferredStyle: .alert)
        
	// 기본 버튼 눌렸을 때 액션
        let action = UIAlertAction(title: "Add Item", style: .default) { action in
            // what will happen once the user clicks the Add Item button on our UIAlert
            self.itemArray.append(textField.text!)
            self.tableView.reloadData()
        }
        
        // 처음 텍스트 입력창이 뜰 때 트리거.
        alert.addTextField { alertTextField in
            textField = alertTextField
        }
        
	// 액션 추가
        alert.addAction(action)
        
	// 얼럿 창 오픈
        present(alert, animated: true, completion: nil)
}
```



### Firebase DB

1.  클라우드 파이어스토어

    spank new DB, more feature
2.  리얼타임 데이터베이스

    only JSON in the cloud

지역 설정할 때, 각 지역별로 네트워크 속도가 다르지만 비용 또한 다를 수 있다는 점 알자.

```swift
import FirebaseFirestore

// 생성
let db = Firestore.firestore()

// 데이터 저장, field in Collection 
if let messageBody = messageTextfield.text, let messageSender = Auth.auth().currentUser?.email {
    db.collection(K.FStore.collectionName).addDocument(data: [
        K.FStore.senderField: messageSender,
        K.FStore.bodyField: messageBody
    ]) { (error) in
        if let e = error {
            print("There was an issue saving data to firestore, \\(e)")
        } else {
            print("Successfully saved data.")
        }
    }
}

// 데이터 읽기, 수동 업데이트, 자동 업데이트 getDocuments -> addSnapshotListener
db.collection(K.FStore.collectionName).getDocuments { (querySnapshot, error) in
    if let e = error {
        print("There was an issue retrieving data from Firesotre. \\(e)")
    } else {
        if let snapshotDocuments = querySnapshot?.documents {
            for doc in snapshotDocuments {
                let data = doc.data()
                if let messageSender = data[K.FStore.senderField] as? String, let messageBody = data[K.FStore.bodyField] as? String {
                    let newMessage = Message(sender: messageSender, body: messageBody)
                    self.messages.append(newMessage)
                    
                    // 클로저는 백그라운드에서 처리 되어 메인스레드에서 처리할 부분을 따로 처리
                    DispatchQueue.main.async {
                        self.tableView.reloadData()
                    }
                }
            }
        }
    }
}


// 현재 유저 확인 후 스타일
if message.sender == Auth.auth().currentUser?.email {
    cell.leftImageView.isHidden = true
    cell.rightImageView.isHidden = false
    cell.messageBubble.backgroundColor = UIColor(named: K.BrandColors.lightPurple)
    cell.label.textColor = UIColor(named: K.BrandColors.purple)
} else {
    cell.leftImageView.isHidden = false
    cell.rightImageView.isHidden = true
    cell.messageBubble.backgroundColor = UIColor(named: K.BrandColors.purple)
    cell.label.textColor = UIColor(named: K.BrandColors.lightPurple)
}


// 데이터 읽고 쓰기 인증 제한
// 아래는 기본 규칙 세트의 몇 가지 예입니다. 유효한 규칙이지만 프로덕션 애플리케이션에는 권장되지 않습니다.
// Allow read/write access on all documents to any user signed in to the application
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```



