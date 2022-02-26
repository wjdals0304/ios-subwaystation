# 지하철 검색 클론 코딩 

- 30개프로젝트로배우는 iOS앱개발 with Swift초격차 패키지Online


<img src ="https://user-images.githubusercontent.com/26668309/149606569-4e840775-fa99-4d2c-843e-475362b07b02.png" width = 30%> <img src ="https://user-images.githubusercontent.com/26668309/149606599-dbd98884-7238-4f67-ab77-0aa363b3a347.png" width = 30%><img src ="https://user-images.githubusercontent.com/26668309/149606613-7fa8aab5-ee30-4abc-96cf-bad13db4d941.png" width = 30%>



# 사용요소 
- searchBar, tableview, colloectionview  
- snapkit, Alamofire


# 새로 배운 내용 

 - UISearchController 

  ```
   let searchController = UISearchController()
   searchController.searchBar.placeholder = "지하철역을 입력해주세요."
        
    //검색창 클릭시 어두운 부분 제거
   searchController.obscuresBackgroundDuringPresentation = false
   searchController.searchBar.delegate = self
        
   navigationItem.searchController = searchController 
   ```
   
 - closer 안에 self 사용 
 
  ``` 
   // 클로즈안에서 self를 사용할 경우는 [weak self] 사용
   // 사용안하면 강한 참조가 되어서 앱이 죽을수 있는 원인이 될 수 있음

   [weak self] response in
   guard let self = self, case .success(let data) = response.result else { return }
                
   self.stations = data.stations
   self.tableView.reloadData()

  ```
  
 - UICollectionView 
  estimatedItemSize ,sectionInset 속성 적용

   ``` 
   
    private lazy var collectionView: UICollectionView = {
        let layout = UICollectionViewFlowLayout()
        layout.estimatedItemSize = CGSize(width: view.frame.width - 32.0 , height: 100.0)
        layout.sectionInset = UIEdgeInsets(top: 16.0, left: 16.0, bottom: 16.0, right: 16.0)
        layout.scrollDirection = .vertical
    
        let collectionView = UICollectionView(frame: .zero, collectionViewLayout: layout)
        collectionView.backgroundColor = .systemBackground
        collectionView.register(StationDetailCollectionViewCell.self, forCellWithReuseIdentifier: "StationDetailCollectionViewCell")
        
        collectionView.dataSource = self
        
        collectionView.refreshControl = refreshControl
        
        return collectionView 
    }()
    
   
   ```
