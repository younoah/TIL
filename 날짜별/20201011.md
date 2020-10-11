## iOS

- API 서버 네트워킹

1. url을 정의한다.
2. session을 정의한다.
3. 정의한 session에 dataTask를 선언하고 url로 연결한다.
4. dataTask의 클로저 안에서 JSON 디코드를 한다.
5. 데이터데스크를 시작한다. `dataTask.resume()`

```swift
func getData() {
        guard let baseUrl = URL(string: "http://127.0.0.1:8000/splitzone/") else { return }
        
        let session = URLSession(configuration: .default)
        let dataTask = session.dataTask(with: baseUrl) {
            (data: Data?, response: URLResponse?, error:Error?) in
            if let error = error {
                print(error.localizedDescription)
                return
            }
            
            guard let data = data else { return }
            
            do{
                let response = try JSONDecoder().decode([SplitZone].self, from: data)
                self.splitZones = response
                
                DispatchQueue.main.async {
                    self.tableView.reloadData()
                }
            } catch(let err) {
                print(err.localizedDescription)
            }
        }
        dataTask.resume()
    }
```

### 