# Infra

## 에이전트 실행 및 모니터링 개요 <a id="user-content-&#xC5D0;&#xC774;&#xC804;&#xD2B8;-&#xC2E4;&#xD589;-&#xBC0F;-&#xBAA8;&#xB2C8;&#xD130;&#xB9C1;-&#xAC1C;&#xC694;-3"></a>

와탭 인프라스트럭처 모니터링은 서버 성능 모니터링 서비스를 제공합니다.

### **구성 파일**

**공통 구성 파일**

| 파일명 | 설명 |
| :--- | :--- |
| ChangeLog.txt | 에이전트의 버전 패치 내역 |
| whatap.conf | 서버의 데이터를 수집할 서버의 주소와 서버의 프로젝트 라이선스 키가 입력되는 파일 |

**Linux 구성 파일**

| 파일명 | 설명 |
| :--- | :--- |
| whatap\_infrad | 데이터 수집 및 전송용 에이전트 |
| whatap\_infrad.pid | 실행 중인 에이전트의 PID 값을 기록한 파일 |
| VERSION | 현재 설치된 에이전트의 버전이 기록된 파일 |

**Windows 구성 파일**

| 파일명 | 설명 |
| :--- | :--- |
| whatap\_infra.exe | 정보를 수집하고 수집된 정보를 서버로 전송하는 프로그램 |
| unins000.\* | 에이전트 삭제 파일 |
| whatap.ico | 와탭 인프라의 아이콘 이미지 |

**에이전트 이름 식별**

와탭은 모니터링 정보 수집 대상인 인프라 서버 식별을 위한 정보로 기본적으로 서버로부터 수집한 정보를 활용합니다. 기본적으로 활용하는 정보는 서버의 호스트명\(hostname\)이 됩니다.

* default: hostname

## 에이전트 설치 및 패키지 업데이트/제거 <a id="user-content-&#xC5D0;&#xC774;&#xC804;&#xD2B8;-&#xC124;&#xCE58;-&#xBC0F;-&#xD328;&#xD0A4;&#xC9C0;-&#xC5C5;&#xB370;&#xC774;&#xD2B8;-&#xC81C;&#xAC70;-1"></a>

와탭 인프라스트럭처 모니터링 서비스를 이용하기 위해서는 모니터링 대상 서버에 와탭 인프라 모니터링 에이전트 설치해야 합니다. 와탭 인프라스트럭처 모니터링 에이전트 설치 방법은 whatap.io 사이트에서 제공하는 명령어를 수행하는 것만으로 설치가 완료됩니다.

### **공통**

#### **프로젝트 생성**

[![570](https://github.com/jinronara/IntegratedManual/raw/master/images/570.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/570.png)

서버를 등록하기 위해 우선 프로젝트를 생성합니다. 추가 버튼을 선택하면 아래와 같이 프로젝트 생성 창이 나타납니다. INFRASTRUCTURE 아이콘을 선택한 뒤, 희망하는 프로젝트명과 데이터 서버 지역, 소속하게 될 그룹을 선택한 뒤 프로젝트를 생성합니다.

[![580](https://github.com/jinronara/IntegratedManual/raw/master/images/580.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/580.png)

#### **라이선스 발급**

[![590](https://github.com/jinronara/IntegratedManual/raw/master/images/590.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/590.png)

에이전트 설치 화면에서 라이선스를 발급 받습니다. 라이선스 키는 프로젝트별로 귀속되기 때문에, 유출되거나 배포되어서는 안됩니다. 반드시 본인 프로젝트에 서버를 등록할 때에만 이용하시기 바랍니다.

### **Debian/Ubuntu**

#### **패키지 저장소\(Repository\) 등록**

와탭 저장소\(Repository\)를 추가합니다.

```text
$ wget http://repo.whatap.io/debian/release.gpg -O -|sudo apt-key add -
$ wget http://repo.whatap.io/debian/whatap-repo_1.0_all.deb
$ sudo dpkg -i whatap-repo_1.0_all.deb
$ sudo apt-get update
```

#### **인프라 모니터링 설치**

아래의 명령어를 입력하여 와탭 인프라 모니터링을 설치합니다.

```text
$ sudo apt-get install whatap-infra
```

#### **라이선스키 및 수집 서버 설정**

아래의 명령어에 발급받은 라이선스 키와 수집 서버 IP를 넣어 입력함으로써 설정을 합니다.

```text
$ echo "license=[라이선스 키]" |sudo tee /usr/whatap/infra/conf/whatap.conf
$ echo "whatap.server.host=[발급된 수집 서버 IP]" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
$ echo "createdtime=`date +%s%N`" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
sudo service whatap-infra restart
```

* 에이전트 설치 페이지에서 발급 받은 명령문에는 라이선스 키가 포함되어 있기 때문에 유출되거나, 배포되지 않도록 주의하시길 바랍니다.
* 에이전트는 수집 서버 주소로 정보를 전송합니다. 그러므로 에이전트가 설치된 서버는 TCP 아웃바운드 포트\(6600\)가 열려 있어야 합니다.

### **Redhat/CentOS/Amazon-Linux**

#### **패키지 저장소\(Repository\) 등록**

와탭 저장소\(Repository\)를 추가합니다.

```text
sudo rpm --import http://repo.whatap.io/centos/release.gpg
sudo rpm -Uvh http://repo.whatap.io/centos/5/noarch/whatap-repo-1.0-1.noarch.rpm
```

**인프라 모니터링 설치**

아래의 명령어를 입력하여 와탭 인프라 모니터링을 설치합니다.

```text
sudo yum install whatap-infra
```

#### 라이선스 수집 서버 설정

```text
$ echo "license=[라이선스 키]" |sudo tee /usr/whatap/infra/conf/whatap.conf
$ echo "whatap.server.host=[발급된 수집 서버 IP]" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
$ echo "createdtime=`date +%s%N`" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
sudo service whatap-infra restart
```

* 에이전트 설치 페이지에서 발급 받은 명령문에는 라이선스 키가 포함되어 있기 때문에 유출되거나, 배포되지 않도록 주의하시길 바랍니다.
* 에이전트는 수집 서버 주소로 정보를 전송합니다. 그러므로 에이전트가 설치된 서버는 TCP 아웃바운드 포트\(6600\)가 열려 있어야 합니다.

### **Windows**

#### **에이전트 다운로드**

에이전트 설치 페이지에서 WINDOWS를 클릭합니다.

[![600](https://github.com/jinronara/IntegratedManual/raw/master/images/600.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/600.png)

whata\_infra.exe 파일을 다운받습니다. 보안 설정으로 인해 .exe형식의 파일을 받지 못할 경우를 대비하여 .zip 형식의 파일로도 다운받을 수 있습니다.

* 서버 보안을 위해 브라우저를 통한 직접 설치보다 다운로드 받은 설치 파일을 실행시키는 것을 권장합니다.

#### **에이전트 업로드**

인프라 모니터링을 설치할 서버에 접속하고, 다운로드 받은 에이전트 파일을 업로드합니다.

#### **에이전트 설치**

서버에서 업로드 받은 파일을 실행합니다.

[![610](https://github.com/jinronara/IntegratedManual/raw/master/images/610.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/610.png)

해당 입력란에 발급받은 라이선스 키와 데이터 서버 주소\(IP\)를 입력합니다. 이후 설치가 완료되면 아래 그림과 같은 화면을 볼 수 있으며, 에이전트가 자동적으로 모니터링을 시작합니다. 버튼을 눌러 설치를 완료합니다.

* 에이전트는 수집 서버 주소로 정보를 전송합니다. 그러므로 수집 서버 주소로 가는 TCP 아웃바운드 포트\(6600\)가 차단되어 있으면 안됩니다.

[![620](https://github.com/jinronara/IntegratedManual/raw/master/images/620.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/620.png)

### **알림 일시 정지**

서버는 운영 중에 확장/유지보수/문제해결/단순 재시작 등의 이유로 잠시 정지해야 할 필요가 있습니다. 이럴 경우 불필요한 오탐을 방지하기 위해 서비스를 잠시 일시정지가 가능합니다.

* 주의: 서비스 일시정지 시에도 요금은 청구됩니다,

[![630](https://github.com/jinronara/IntegratedManual/raw/master/images/630.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/630.png)

모니터링 중인 서버들 중 일시정지하고자 하는 서버를 선택합니다. 일시정지하고자 하는 서버 선택 후 우측 상단에 있는 액션을 클릭하면 드롭다운 메뉴가 나오는 것이 확인 가능합니다. 해당 메뉴에서 일시정지 버튼을 클릭할 경우 알림이 나가지 않습니다.

* 일시정지 기간 동안에는 데이터가 수집되지만 알림이 발생하지 않습니다.

### **알림 재시작**

서버 작업 완료 후 알림 발송을 재개하기 위해서는 재시작 하길 원하는 서버를 선택 후 액션을 클릭하여 나오는 드롭다운 메뉴에서 재시작 버튼을 클릭하여 알림 발송을 재개합니다.

### **해지**

모니터링이 더 이상 필요하지 않을 경우 와탭 에이전트를 손쉽게 해지할 수 있습니다. 해지를 희망하는 서버를 선택한 후, 액션 버튼을 클릭하여 나오는 드롭다운 메뉴에서 해지 버튼을 누르면 아래 그림과 같은 팝업창을 확인 할 수 있습니다.[![630](https://github.com/jinronara/IntegratedManual/raw/master/images/630.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/630.png)

해당 팝업 창에서 해지를 누를 경우 서버가 해지됩니다.

* 주의 : 모니터링 해지 시 해당되는 수집 서버에 저장된 데이터가 즉시 사라져 보고서와 같은 서비스를 받으실 수 없습니다. 따라서 삭제 전 신중하게 결정하여 해지해주시길 바랍니다.

### **제거**

와탭 콘솔상에서 서버 해지를 완료 하였다면, 서버 상에서도 에이전트 삭제가 필요합니다.

#### **Debian/Ubuntu**

```text
$ apt-get remove whatap-infra
```

* 남아있는 설정파일은 /usr/whatap에 있습니다. 해당 whatap 폴더를 지워주시면 됩니다.

#### **Redhat/CentOS/Amazon-Linux**

```text
$ yum remove whatap-infra
```

* 남아있는 설정파일은 /usr/whatap에 있습니다. 해당 whatap 폴더를 지워주시면 됩니다.

#### **Windows**

제어판 → 프로그램 추가/제거에서 인프라 모니터링을 찾아서 삭제하시거나 와탭 설치 경로인 C:\Program Files\WhatapInfra 에서 unins000.exe를 실행하여 삭제하셔도 됩니다.

## FAQ <a id="user-content-faq-4"></a>

### **업그레이드**

#### **윈도우 버전 업그레이드**

기존 와탭 인프라 에이전트 프로그램을 삭제하지 말고 설치 파일을 실행하면 자동으로 업그레이드 됩니다.

#### **Ubuntu 계열**

아래와 같이 실행합니다.

```text
apt-get update
apt-get install whatap-infra
```

#### **Redhat 계열**

아래와 같이 실행합니다.

```text
yum check-update
yum install whatap-infra
```

### **인터넷 연결이 안되는 서버에 설치**

#### **Windows OS**

1.아래 주소에서 설치 파일을 다운로드 받습니다. 

```text
http://repo.whatap.io/windows/whatap.zip
```

2. 프로젝트 설치 안내 페이지 안내에 따라 설치 진행 합니다. 

#### **Ubuntu OS**

1.아래 주소에서 설치 파일을 다운로드 받습니다. 

```text
http://repo.whatap.io/debian/unstable/whatap-infra_1.1.2_amd64.deb
```

2. 설치 명령을 수행합니다. 

```text
sudo dpkg -i whatap-infra_1.1.2_amd64.deb
```

3. 프로젝트 설치 안내 페이지 안내에 따라 설 진행 합니다. 

#### **CentOS/RedHat/AmazonLinux**

1.아래 주소에서 설치 파일을 다운로드 받습니다. 

```text
# Centos 6.x
http://repo.whatap.io/centos/6/x86_64/whatap-infra-1.1-2.x86_64.rpm

# Centos 7.x
http://repo.whatap.io/centos/7/x86_64/whatap-infra-1.1-2.x86_64.rpm
```

2. 설치 명령을 수행합니다. 

```text
sudo rpm -Uvh whatap-infra-1.1-2.x86_64.rpm
```

3. 프로젝트 설치 안내 페이지 안내에 따라 설정 진행 합니다. 

### **최신버젼 확인**

#### **Ubuntu/Debian**

아래 명령을 터미널에서 실행합니다.

```text
apt-cache showpkg whatap-infra
```

#### **CentOS/RedHat/AmazonLinux**

아래 명령을 터미널에서 실행합니다.

```text
yum info whatap-infra
```

## 설치 에러 대응

### **설치 후 서버 목록에 표시되지 않을 때**

#### **Windows**

Cmd 창에서 아래 명령을 수행 하면 오류 원인을 파악할 수 있습니다.

```text
“C:\Program Files\WhatapInfra\whatap_infra.exe” –whatapip {수집서버 IP} –license {라이선스 문자열} test
```

#### **Linux**

터미널에서 아래 명령을 수행하면 오류 원인을 파악 할 수 있습니다.

```text
/usr/whatap/infra/whatap_infrad –whatapip {수집서버 IP}—license {라이선스 문자열} test
```

## 제약 사항 <a id="user-content-&#xC81C;&#xC57D;-&#xC0AC;&#xD56D;-4"></a>

제약사항 없음

## 호환성 목록 <a id="user-content-&#xD638;&#xD658;&#xC131;-&#xBAA9;&#xB85D;-3"></a>

* Debian 7.0 이상
* Ubuntu 12.04 이상
* CentOS 6 이상
* RHEL 6 이상
* Amazon Linux
* Windows Server 2008 R2 SP2 이상

