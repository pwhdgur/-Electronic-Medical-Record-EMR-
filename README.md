# Electronic-Medical-Record (EMR)

< Hyperledger Fabric 1.4 Electronic Medical Record(EMR) Sample Application V1.0 >

1. Chaincode (go)
진료차트 정보 : 차트번호(EMR OO), 이름, 생년월일(주민번호), 성별, 나이, 전화번호, 주소, 상병(고혈압, 당뇨, 간염, 엘러지, 수술 등), 진찰소견, 상병명, 처방(약품병, 용량, 횟수, 투약일수 등)

type Car struct {
	Make   string `json:"make"`
	Model  string `json:"model"`
	Colour string `json:"colour"`
	Owner  string `json:"owner"`
}

type EMR struct {
	Name   string `json:"name"`
	DateOfBirth  string `json:"dateofbirth"`
	Sex string `json:"sex"`
	PhoneNumber  string `json:"phonenumber"`
	Address  string `json:"address"`
	Sickness  string `json:"sickness"`
	MedicalExamin  string `json:"medicalexamin"`
	Prescription  string `json:"prescription"`
}


cars := []Car{
		Car{Make: "Toyota", Model: "Prius", Colour: "blue", Owner: "Tomoko"},
		Car{Make: "Ford", Model: "Mustang", Colour: "red", Owner: "Brad"},
		Car{Make: "Hyundai", Model: "Tucson", Colour: "green", Owner: "Jin Soo"},
		Car{Make: "Volkswagen", Model: "Passat", Colour: "yellow", Owner: "Max"},
		Car{Make: "Tesla", Model: "S", Colour: "black", Owner: "Adriana"},
		Car{Make: "Peugeot", Model: "205", Colour: "purple", Owner: "Michel"},
		Car{Make: "Chery", Model: "S22L", Colour: "white", Owner: "Aarav"},
		Car{Make: "Fiat", Model: "Punto", Colour: "violet", Owner: "Pari"},
		Car{Make: "Tata", Model: "Nano", Colour: "indigo", Owner: "Valeria"},
		Car{Make: "Holden", Model: "Barina", Colour: "brown", Owner: "Shotaro"},
	}

cars := []EMR{
		EMR{Name: "Daniel", DateOfBirth: "2000-02-03", Sex: "M", PhoneNumber: "0101112222", Address: "Samsung-dong, seoul", Sickness: "COVID-19", MedicalExamin: "Underlying disease", Prescription: "Intravenous(IV)"},
		EMR{Name: "Michle", DateOfBirth: "1995-05-01", Sex: "M", PhoneNumber: "0102223333", Address: "Secho-dong, seoul", Sickness: "COLD", MedicalExamin: "influenza", Prescription: "Tamiflu"},
		EMR{Name: "Grace", DateOfBirth: "1982-12-15", Sex: "F", PhoneNumber: "0103335555", Address: "suji-dong, yongin-city", Sickness: "pneumonia", MedicalExamin: "Chonic cough", Prescription: "Antibiotic"},
}

var car = Car{Make: args[1], Model: args[2], Colour: args[3], Owner: args[4]}
var car = EMR{Name: args[1], DateOfBirth: args[2], Sex: args[3], PhoneNumber: args[4], Address: args[5], Sickness: args[6], MedicalExamin: args[7], Prescription: args[8]}

await contract.submitTransaction('createCar', 'CAR12', 'Honda', 'Accord', 'Black', 'Tom');
await contract.submitTransaction('createCar', 'EMR11', 'Tom', '2000-01-01', 'M', '0106667777', 'Pangyo-dong, seongnam-city', 'headache', 'Acute Stress Disorder', 'aspirin');


2. fabric network v1.4
버전별 이미지 다운도드 
curl -sSL http://bit.ly/2ysbOFE | bash -s -- 1.4.6 1.4.6 0.4.18
curl -sSL https://bit.ly/2ysbOFE | bash -s -- 2.0.1 1.4.6 0.4.18

$ ./startFabric.sh
- 1개 orderer.example.com
- 2개 org1.example.com/org2.example.com
- 4개 peer0.org1.example.com/peer1.org1.example.com/peer0.org2.example.com/peer1.org2.example.com
- 2개 ca_peerOrg1/ca_peerOrg2
- 4개 couchdb0/couchdb1/couchdb2/couchdb3
- 1개 cli

3. REST API Server Side
@# app.js

/*
  if ((typeof req.body.key === 'undefined' || req.body.key === '') ||
      (typeof req.body.make === 'undefined' || req.body.make === '') ||
      (typeof req.body.model === 'undefined' || req.body.model === '') ||
      (typeof req.body.color === 'undefined' || req.body.color === '') ||
      (typeof req.body.owner === 'undefined' || req.body.owner === '')) {
    res.json({status: false, error: {message: 'Missing body.'}});
    return;
  }
*/

  if ((typeof req.body.key === 'undefined' || req.body.key === '') ||
      (typeof req.body.name === 'undefined' || req.body.name === '') ||
      (typeof req.body.dateofbirth === 'undefined' || req.body.dateofbirth === '') ||
      (typeof req.body.sex === 'undefined' || req.body.sex === '') ||
	  (typeof req.body.phonenumber === 'undefined' || req.body.phonenumber === '') ||
	  (typeof req.body.address === 'undefined' || req.body.address === '') ||
	  (typeof req.body.sickness === 'undefined' || req.body.sickness === '') ||
	  (typeof req.body.medicalexamin === 'undefined' || req.body.medicalexamin === '') ||
      (typeof req.body.prescription === 'undefined' || req.body.prescription === '')) {
    res.json({status: false, error: {message: 'Missing body.'}});
    return;
  }

//    await contract.submitTransaction('createCar', req.body.key, req.body.make, req.body.model, req.body.color, req.body.owner);
	await contract.submitTransaction('createCar', req.body.key, req.body.name, req.body.dateofbirth, req.body.sex, req.body.phonenumber, req.body.address, req.body.sickness, req.body.medicalexamin, req.body.prescription);

/*
  if ((typeof req.body.key === 'undefined' || req.body.key === '') ||
      (typeof req.body.owner === 'undefined' || req.body.owner === '')) {
    res.json({status: false, error: {message: 'Missing body.'}});
    return;
  }
*/

  if ((typeof req.body.key === 'undefined' || req.body.key === '') ||
      (typeof req.body.prescription === 'undefined' || req.body.prescription === '')) {
    res.json({status: false, error: {message: 'Missing body.'}});
    return;
  }

//	await contract.submitTransaction('changeCarOwner', req.body.key, req.body.owner);
    await contract.submitTransaction('changeCarOwner', req.body.key, req.body.prescription);

4. Application Side

@# fabcar-client
1. nano App.js //화면 내의 명칭변경.

2. nano AllCars.js
<td>{car.Record.make}</td>
<td>{car.Record.model}</td>
<td>{car.Record.color}</td>
<td>{car.Record.owner}</td>

=> 변경
<td>{car.Record.name}</td>
<td>{car.Record.dateofbirth}</td>
<td>{car.Record.sex}</td>
<td>{car.Record.phonenumber}</td>
<td>{car.Record.address}</td>
<td>{car.Record.sickness}</td>
<td>{car.Record.medicalexamin}</td>
<td>{car.Record.prescription}</td>

<th>Key</th>
<th>Make</th>
<th>Model</th>
<th>Color</th>
<th>Owner</th>

=> 변경
<th>Key</th>
<th>Name</th>
<th>Date of Birth</th>
<th>Sex</th>
<th>Phonenumber</th>
<th>Address</th>
<th>Sickness</th>
<th>Medical Examination</th>
<th>Prescription</th>

3. nano AllCars.js

this.state = {
    key: '',
    make: '',
    model: '',
    color: '',
    owner: '',
    redirect: false
}

=> 변경
this.state = {
    key: '',
    name: '',
    dateofbirth: '',
    sex: '',
    phonenumber: '',
	address: '',
	sickness: '',
	medicalexamin: '',
	prescription: '',
    redirect: false
}


onKeyChanged(e) { this.setState({ key: e.target.value.toUpperCase() }) }
onMakeChanged(e) { this.setState({ make: e.target.value }) }
onModelChanged(e) { this.setState({ model: e.target.value }) }
onColorChanged(e) { this.setState({ color: e.target.value }) }
onOwnerChanged(e) { this.setState({ owner: e.target.value }) }

=> 변경
onKeyChanged(e) { this.setState({ key: e.target.value.toUpperCase() }) }
onNameChanged(e) { this.setState({ name: e.target.value }) }	
onDateofBirthChanged(e) { this.setState({ dateofbirth: e.target.value }) }
onSexChanged(e) { this.setState({ sex: e.target.value }) }
onPhonenumberChanged(e) { this.setState({ phonenumber: e.target.value }) }
onAddressChanged(e) { this.setState({ address: e.target.value }) }
onSicknessChanged(e) { this.setState({ sickness: e.target.value }) }
onMedicalExaminChanged(e) { this.setState({ medicalexamin: e.target.value }) }
onPrescriptionChanged(e) { this.setState({ prescription: e.target.value }) }


key: this.state.key,
make: this.state.make,
model: this.state.model,
color: this.state.color,
owner: this.state.owner

=> 변경
key: this.state.key,
name: this.state.name,
dateofbirth: this.state.dateofbirth,
sex: this.state.sex,
phonenumber: this.state.phonenumber,
address: this.state.address,
sickness: this.state.sickness,
medicalexamin: this.state.medicalexamin,
prescription: this.state.prescription

< Hyperledger Fabric 1.4 The Operations Service >
- Log Level Management [/logspec]
- Health Check [/healthz]
- Metrics [/metrics]

1. Configuration
1.1 peer와 orderer의 설정 파일에서 listenAddress, metrics provider와 TLS 설정을 확인 및 변경
- peer: fabric-samples/config/core.yaml
- orderer: fabric-samples/config/orderer.yaml

1.2 모니터링을 위한 container(peer 및 orderer) 환경 변수 설정: ~/fabric-samples/first-network/base/docker-compose-base.yaml
- CORE_OPERATIONS_LISTENADDRESS
- CORE_METRICS_PROVIDER
설정을 끝냈다면 byfn network를 실행 후 cli container로 접속한다.

@# change directory
$ cd ~/first-network

@# byfn network start
$ ./byfn.sh up

@# cli container로 접속
$ docker exec -it cli bash

2. logspec API
@# curl command로 peer0.org1.example.com에 logspec API 요청(GET)
$ curl peer0.org1.example.com:9443/logspec
{"spec":"info"}

@# docker container 안에서 설치 명령어 실행
$ apk add curl

3. healthz API
@# orderer.example.com에 healthz API 요청(GET)
$ curl orderer.example.com:8443/healthz
{"status":"OK","time":"2020-03-02T06:36:26.278635314Z"} 

4. metrics API
@# peer0.org1.example.com에 metrics API 요청(GET)
$ curl peer0.org1.example.com:9443/metrics


< Hyperledger Fabric 1.4 Monitoring with Prometheus :  not O.K>

1. 개발 환경
Ubuntu 18.04 LTS
Hyperledger Fabric v2.0.0
prometheus 2.16.0.linux-amd64

2. 다운로드
https://prometheus.io/download/ 접속하여 자신의 운영체제에 맞는 최신 버전의 프로메테우스를 다운로드 받는다. 다운로드 경로를 ~/fabric-samples로 설정하였음.

3. byfn 네트워크 연동을 위한 프로메테우스 설정
$ cd ~/fabric-samples
$ tar -xzvf prometheus-2.17.2.linux-amd64.tar.gz
$ cd prometheus-2.16.0.linux-amd64
$ vi prometheus.yml

byfn 네트워크 모니터링을 위해 scrape_configs의 job_name과 targets 속성을 아래와 같이 수정한다.
- targets: 모니터링할 피어와 오더러 정보를 입력. (예제에서는 4개의 peer와 1개의 orderer를 대상으로 모니터링을 진행)

- job_name: 'hyperledger_metrics'
    scrape_interval: 10s
	static_configs:
		  - targets: [‘peer0.org1.example.com:9443’, ‘peer1.org1.example.com:9443’, ‘peer0.org2.example.com:9443’, ‘peer1.org2.example.com:9443’, ‘orderer.example.com:8443’]

4. byfn 및 prometheus-server 구동
$ cd ..
$ cd first-network

@# Bring up the byfn network
$./byfn up

@# Run the prometheus-server container
$ sudo docker run -d --name prometheus-server -p 9090:9090 --restart always -v /home/ubuntu/fabric_samples/prometheus-2.17.2.linux-amd64/prometheus.yml:/prometheus.yml prom/prometheus --config.file=/prometheus.yml
$ docker ps -a

5. byfn과 prometheus-server 연결
네트워크의 이름은 docker inspect 명령을 통해 찾을 수 있다.

@#docker network connect <network_name> <container ID of prometheus-server>

$ docker inspect orderer.example.com
$ docker network connect net_byfn 93736b947511

6. Web Server UI

http:///localhost:9090

http://13.125.192.135:9090


< Hyperledger Fabric 1.4 Monitoring with Blockchain Explorer - First-Network >
https://tmjb.tistory.com/15

1. first-network 구동

$ cd ~/fabric-samples/first-network
$ ./byfn.sh generate
$ ./byfn.sh up

2. 블록체인 익스플로러 소스 다운로드
$ git clone https://github.com/hyperledger/blockchain-explorer.git

3. 포스트그레스 데이터베이스 설치
$ sudo apt-get update
$ sudo apt-get install postgresql postgresql-contrib
$ service postgresql restart

3.1 PostgreSQL 명령어
    - DATABASE 삭제
    DROP DATABASE name;
	
	- 계정삭제
	DROP ROLE 계정명;
	
	- 계정 리스트
	/du
	
	- DB 변경
	/c databasename
	
3.2 postgres password 설정 및 재구동, 확인
	$ sudo -u postgres psql
	$ postgres=# ALTER USER postgres with encrypted password '123qwe';
	$ ALTER ROLE
	$ postgres=# \q
	$ sudo service postgresql restart
	$ netstat -ntl 5432
	
	2.1 정상설치 여부 
	$ dpkg -l | grep postgres
	
	2.2 관리자 계정
	$ cat /etc/passwd | grep postgres
	
	2.3 실행상태 여부
	$ /etc/ini.d/postgresql status
	
3.3 상태확인 명령어
$ pg_lsclusters

3.4 Database Setup
	$ cd blockchain-explorer/app
	Modify explorerconfig.json
	Modify 예제는 아래
	{
		"persistence": "postgreSQL",
		"platforms": ["fabric"],
		"postgreSQL": {
			"host": "127.0.0.1",
			"port": "5432",
			"database": "fabricexplorer",
			"username": "hppoc",
			"passwd": "123qwe"
		},
		sync": {
			"type": "host",   /* "type": "local", */
			"platform": "fabric",
			"blocksSyncTime": "3"
		}
	}
	
	$ cd block-explorer/
	Modify $nano appconfig.json
	Modify 예제는 아래
	{
		/* "host": "localhost", *
		"host": "www.devhyperledger.com",
		"port": "8089",
		"license": "Apache-2.0"
	}

4. 데이터베이스 에 기본 구성(테이블, 데이터 등) 생성

$ cd blockchain-explorer/app/persistence/fabric/postgreSQL
$ chmod -R 775 db/
$ cd db
$ ./createdb.sh

@# 생성 리스트 확인 명령어 (/c fabricexplorer : DB 변경, \l : view created fabricexplorer database, \d : view created tables 등 명령어로 확인해봄)
$ sudo -u postgres psql
$ \l

@# exit command
$ /q

5. 익스플로러 설정 파일 수정
아래 경로에 위치한 파일의 주소를 기억 해 둡니다.
$ ls ~/fabric-samples/first-network/crypto-config/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp/keystore/
(ex : 6dcad9a5f35df0d85956ffb2365fd3f0515342e345676442ac0edb872bbb71e9_sk)
ba03feaf427fe98d2d96209fcb2c097f4adfd643022dfc28c7082e1227fe179c_sk
ba03feaf427fe98d2d96209fcb2c097f4adfd643022dfc28c7082e1227fe179c_sk


해당 경로에 위치한 json 설정 파일을 열어 기억 해 두었던 파일 path 로 대체 (organizations - adminPrivateKey, signedCert 2가지 key path , peers - tlsCACerts key path)
$ cd blockchain-explorer/app/platform/fabric/connection-profile
$ vi first-network.json
@## 수정파일 내용
 "organizations": {
                "Org1MSP": {
                        "mspid": "Org1MSP",
                        "adminPrivateKey": {
                                "path": "/fabric-path/fabric-samples/first-network/crypto-config/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp/keystore/1bebc656f198efb4b5bed08ef42cf3b2d89ac_sk"
						수정내용 =>"path": "/home/ubuntu/fabric-samples/first-network/crypto-config/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp/keystore/6dcad9a5f35df0d85956ffb2365fd3f0515342e345676442ac0edb872bbb71e9_sk"
						},
                        "signedCert": {
                                "path": "/fabric-path/fabric-samples/first-network/crypto-config/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp/signcerts/Admin@org1.example.com-cert.pem"
						수정내용 =>"path": "/home/ubuntu/fabric-samples/first-network/crypto-config/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp/signcerts/Admin@org1.example.com-cert.pem"		
                        }
                }
        },
        "peers": {
                "peer0.org1.example.com": {
                        "tlsCACerts": {
                                "path": "/fabric-path/fabric-samples/first-network/crypto-config/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt"
						수정내용 =>"path": "/home/ubuntu/fabric-samples/first-network/crypto-config/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt"		
                        },
                        "url": "grpcs://localhost:7051",
                        "grpcOptions": {
                                "ssl-target-name-override": "peer0.org1.example.com"
                        }
                }
        }


5. 익스플로러 설치 스크립트 실행 및 기동
$ cd blockchain-explorer
$ ./main.sh install
$ ./start.sh

//로그 확인하기 
$ tail -f logs/app/app.log 

6. Web Server UI

http://www.devhyperledger.com:8089

설치가 정상적으로 완료 되었다면 http://<Your-IP-Address>:8089 웹사이트로 억세스 할 수 있습니다.
처음접속하면 아이디와 비번 입력하는 화면이 뜨는데 해당 정보는 3.4번에서 설정 했던 first-network.json 파일에 기입 되어 있습니다. (디폴트는 admin:adminpw)


< Clear System >
1. docker command

@# List
$ docker ps -a --format="table {{.ID}}\t{{.Names}}\t{{.Image}}\t{{.Status}}\t{{.Ports}}"
$ docker ps -a --format="table {{.ID}}\t{{.Names}}\t{{.Image}}\t{{.Status}}"

@# 실행 중인 docker container 모두 종료
$ docker rm -f $(docker ps -aq)

@# dev-* 이미지만 삭제 
$ docker rmi $(docker images dev-* -q)

@# docker container에서 사용하지 않는 모든 docker volume을 삭제
$ docker volume prune

@# cached network 초기화
$ docker network prune

@# 모든 이미지 삭제 
$ docker rmi -f $(docker images -q)

2. nodejs 데몬실행 command

@# forever install
$ sudo npm install forever -g

@# forever 사용법
$ forever start [js script]
$ forever list
$ forever stop [js script/pid/id]

@# forever damone
$ forever start -c "npm start" ./

3. Domain
www.devhyperledger.com

4. 기타 명령어
- ifconfig (IP)
- netstat -ntl (Port)
- sudo rebbot
- df -h
- find / -name '.bash*'
- apt --installed list
- ps -ef
- ps -ef | grep httpd
- printenv (환경변수 보기)
- netstat -tnlp
- chown -R bbb:bbb /home/bbb/dev/test  (하위 디렉토리까지 소유권 변경)
- docker exec -it c456623444b1 /bin/bash  (컨테이너 접속)
- kill -INT 123

$ netstat -nap | grep 3000
@# fuser -k -n tcp 3000

curl -sSL http://bit.ly/2ysbOFE | bash -s -- 1.4.6 1.4.6 0.4.18

curl -sSL https://bit.ly/2ysbOFE | bash -s -- 2.0.1 1.4.6 0.4.18
