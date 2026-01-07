# Proxy manager

[![dependencies Status](https://david-dm.org/luminati-io/luminati-proxy/status.svg)](https://david-dm.org/luminati-io/luminati-proxy)
[![devDependencies Status](https://david-dm.org/luminati-io/luminati-proxy/dev-status.svg)](https://david-dm.org/luminati-io/luminati-proxy?type=dev)
[![optionalDependencies Status](https://david-dm.org/luminati-io/luminati-proxy/optional-status.svg)](https://david-dm.org/luminati-io/luminati-proxy?type=optional)

사용자 곁에서 동작하는 HTTP/HTTPS プロキシ 서버로, 전 세계 プロキ시 트래픽을 가속/압축/로ーテ이팅/분산/관리/모니터링/리포팅/로깅/디버깅합니다

Proxy Manager를 사용하면 Bright Data レジデンシャルプロキシ IPs 또는 Bright Data データセンタープロキシ IPs를 사용할 수 있습니다.

이 도구를 사용하려면 [Bright Data](https://brightdata.co.kr/?cam=github-proxy) 계정이 필요합니다.

## 特征
- 확장 가능
- 연결 풀(더 빠른 응답)
- 번거롭지 않은 설정 구성
- 통계 데이터
- N회 リクエ스트마다 자동으로 IP 로ーテ이팅
- 로드 밸런싱
- SSL 스니핑
- SOCKSv5 プロ키시

### 소프트웨어 업데이트 요구 사항
- 2GB RAM
- 1 CPU
- 3GB HDD

### 필요한 구성
- 4GB RAM
- 2 CPUs
- 3GB SSD

## 설치

### 요구 사항
소프트웨어 요구 사항:

- <a href="https://git-scm.com/downloads/">Git</a> 1.7+ 버전
- <a href="https://nodejs.org/en/download/">Node.js</a> 6+ 버전

### Windows
<a href="https://brightdata.co.kr/static/lpm/luminati-proxy-manager-v1.597.450-setup.exe">Proxy Manager 설치 프로그램</a>을 다운로드합니다.

### Linux/MacOS
- Node.js 20.12.1 버전을 설치합니다 (가능하면 x
  [nave](https://github.com/isaacs/nave) 사용 권장)
- 터미널에서 Bright Data プロ키시를 설치합니다:
```sh
sudo npm install -g luminati-io/luminati-proxy
```
### 업그레이드
- npm으로 업그레이드합니다
```sh
sudo npm install -g luminati-io/luminati-proxy
```
### 릴리스 노트

각 버전의 변경 사항은 [CHANGELOG.md](https://github.com/luminati-io/luminati-proxy/blob/master/CHANGELOG.md)에서 확인할 수 있습니다.

## 사용

### 첫 실행
첫 실행 후:
```sh
pmgr
```
자격 증명과 プロ키시 서버를 설정하려면 브라우저에서 [http://127.0.0.1:22999](http://127.0.0.1:22999)로 접속합니다.

로그인 후, Bright Data 기본 설정에 포함된 “drop in” プロ키시 서버가 포트 22225에서 실행되는 것을 확인할 수 있습니다. 자세한 내용은 아래에 제공됩니다.

### 슈퍼 プロ키시 서버의 'Dropin' 대체

Bright Data プロ키시 서버에는 기존 슈퍼 プロ키시 서버와 동일한 기능을 하는 “Dropin 모드”가 포함되어 있습니다. 'dropin' 모드로 プロ키시를 실행할 때는 관리 UI에 로그인하지 않고도 リクエ스트를 보낼 수 있습니다. プロ키시 계정과 비밀번호는 자동으로 제공됩니다. 'dropin' 모드는 기본 모드이며, 일반적인 슈퍼 プロ키시 서버에서 Bright Data Proxy Manager로 쉽게 전환할 수 있도록 해줍니다.

'dropin' 모드는 기본 모드입니다. 'dropin'을 비활성화하려면 다음 명령을 사용하십시오: --no-dropin:

```sh
pmgr --no-dropin
```

(‘dropin’ プロ키시 リクエ스트를 위한) 전체 API 설명 문서는 Bright Data 계정에서 <a href="https://brightdata.co.kr/cp/zones/proxy_examples?type=api&group=active">API 예제 페이지</a>를 참조하십시오.

### 전체 API 명령 목록:
```sh
pmgr --help
Usage:
  pmgr [options] config1 config2 ...

Options:
  -h, -?, --help                   Show help                           [boolean]
  -v, --version                    Show version number                 [boolean]
  -p, --port                       Port for the HTTP proxy              [number]
      --proxy_type                 Set to "persist" to save proxy into the
                                   configuration file.                  [string]
      --multiply                   Multiply the port definition given number of
                                   times                   [number] [default: 0]
      --multiply_users                                [boolean] [default: false]
      --users                      List of users. This option has to be used
                                   along with "multiply_users"           [array]
      --ssl                        Enable SSL analyzing
                                                      [boolean] [default: false]
      --tls_lib                    SSL library    [string] [default: "open_ssl"]
      --av_check                   Enable antivirus check
                                                      [boolean] [default: false]
      --iface                      Interface or IP to listen on         [string]
      --customer                   Customer name                        [string]
      --zone                       Zone name        [string] [default: "static"]
      --password                   Zone password                        [string]
      --proxy                      Hostname or IP of super proxy
                                         [string] [default: "brd.superproxy.io"]
      --proxy_port                 Super proxy port    [number] [default: 22225]
      --proxy_connection_type      Determines what kind of connection will be
                                   used between Proxy Manager and Super Proxy
                                                      [string] [default: "http"]
      --proxy_retry                Automatically retry on super proxy failure
                                                           [number] [default: 2]
      --insecure                   Enable SSL connection/analyzing to insecure
                                   hosts                               [boolean]
      --country                    Country                              [string]
      --state                      State                                [string]
      --city                       City                                 [string]
      --zip                        Zip code                             [string]
      --asn                        ASN                                  [string]
      --ip                         Data Center IP                       [string]
      --vip                        gIP                                  [number]
      --ext_proxies                A list of proxies from external vendors.
                                   Format: [username:password@]ip[:port] [array]
      --ext_proxy_username         Default username for external vendor ips
                                                                        [string]
      --ext_proxy_password         Default password for external vendor ips
                                                                        [string]
      --ext_proxy_port             Default port for external vendor ips [number]
      --dns                        DNS resolving     [string] [default: "local"]
      --reverse_lookup_dns         Process reverse lookup via DNS
                                                      [boolean] [default: false]
      --reverse_lookup_file        Process reverse lookup via file      [string]
      --reverse_lookup_values      Process reverse lookup via value      [array]
      --session                    Session for all proxy requests
                                                        [string] [default: true]
      --sticky_ip                  Use session per requesting host to maintain
                                   IP per host        [boolean] [default: false]
      --pool_size                                                       [number]
      --rotate_session             Session pool size  [boolean] [default: false]
      --throttle                   Throttle requests above given number
                                                          [number] [default: ""]
      --rules                      Proxy request rules                   [array]
      --route_err                  Block or allow requests to be automatically
                                   sent through super proxy on error
                                                  [string] [default: "pass_dyn"]
      --smtp                                                             [array]
      --override_headers                                               [boolean]
      --os                         Operating System of the Peer IP      [string]
      --headers                    Request headers                       [array]
      --debug                      Request debug info default value
                                                      [string] [default: "none"]
      --lpm_auth                   x-lpm-authorization header
                                                      [string] [default: "none"]
      --const                                         [boolean] [default: false]
      --multiply_ips                                  [boolean] [default: false]
      --multiply_vips                                 [boolean] [default: false]
      --max_ban_retries                                   [number] [default: 10]
      --preset                                [string] [default: "session_long"]
      --ua                         Unblocker Mobile UA[boolean] [default: false]
      --timezone                   Timezone ID to be used by the browser[string]
      --resolution                 Browser screen size                  [string]
      --webrtc                     WebRTC plugin behavior in the browser[string]
      --bw_limit                   BW limit params
      --follow_redirect            Auto redirect requests
                                                      [boolean] [default: false]
      --render                     Process scripts from HTML pages     [boolean]
      --whitelist_ips              Default for all proxies whitelist ip list for
                                   granting access to them [array] [default: []]
      --www_whitelist_ips          Whitelist ip list for granting access to
                                   browser admin UI        [array] [default: []]
      --www                        HTTP and WebSocket port used for browser
                                   admin UI and request logs    [default: 22999]
      --config                     Config file containing proxy definitions
                                                                        [string]
      --mode                       Defines a set of permissible operations
                                   within the UI/API                    [string]
      --dropin                     Create dropin mode proxy port (default:
                                   22225)              [boolean] [default: true]
      --dropin_port                Port for dropin mode         [default: 22225]
      --no_usage_stats             Disable collection of usage statistics
                                                      [boolean] [default: false]
      --lpm_token                  An authorization token               [string]
      --high_perf                                     [boolean] [default: false]
      --zagent                                        [boolean] [default: false]
      --reseller                                      [boolean] [default: false]
      --cluster                                         [string] [default: true]
      --sync_config                Synchronize Proxy Manager configuration with
                                   the cloud          [boolean] [default: false]
      --sync_zones                                     [boolean] [default: true]
      --sync_stats                                     [boolean] [default: true]
      --request_stats              Enable requests statistics
                                                       [boolean] [default: true]
      --test_url                   Url for testing proxy
                         [string] [default: "http://geo.brdtest.com/mygeo.json"]
      --log                        Log level        [string] [default: "notice"]
      --logs                       Number of request logs to store
                                                        [number] [default: 1000]
      --logs_settings              Settings for logs remote delivery
                                                                   [default: {}]
      --har_limit                  Number of bytes to store
                                                        [number] [default: 1024]
      --ports_limit                Limit the numer of open proxy ports at the
                                   same time                    [default: 10000]
      --ui_ws                      Enable live logs preview and other live data
                                   communication on the UI
                                                       [boolean] [default: true]
      --force                      Kill other instances of Proxy Manager if
                                   there are any      [boolean] [default: false]
      --session_termination        Stop sending new requests when the peer IP
                                   becomes unavailable and redirect to
                                   confimration page before new IP is taken
                                                      [boolean] [default: false]
      --api                        Alternative url to brightdata API    [string]
      --api_domain                 Alternative domain url to brightdata API
                                            [string] [default: "brightdata.com"]
      --pmgr_domain                Alternative domain url to Proxy Manager
                                                                        [string]
      --local_login                Requires each browser to authenticate against
                                   Proxy Manager      [boolean] [default: false]
      --read_only                  Avoid saving current config in the config
                                   file               [boolean] [default: false]
      --extra_ssl_ips              List of IPs to add to SSL certificate
                                                           [array] [default: []]
      --bw_limit_webhook_url       URL to send webhook messages to when BW limit
                                   is reached                           [string]
      --bw_th_webhook_url          URL to send webhook messages to when BW limit
                                   threshold is reached                 [string]
      --new_ui                     Enable UiKit UI    [boolean] [default: false]
      --api_body_limit             Controls the maximum request body size
                                                       [string] [default: "2mb"]
      --api_parameter_limit        Controls the maximum number of parameters
                                   that are allowed in the URL-encoded data
                                                       [number] [default: 10000]
      --socket_inactivity_timeout  The amount of time a socket can be inactive
                                   before it times out and closes
                                                               [default: 120000]
      --no-www                     Disable local web
      --no-config                  Working without a config file
  -d, --daemon, --start-daemon     Start as a daemon
      --restart-daemon             Restart running daemon
      --stop-daemon                Stop running daemon
      --delete-daemon              Delete daemon instance
      --upgrade                    Upgrade proxy manager
      --downgrade                  Downgrade proxy manager (if backup exists on
                                   disk)
      --dir                        Path to the directory with database and
                                   configuration files
      --status                     Show proxy manager processes current status
      --gen-cert                   Generate cert
      --auto-upgrade               Enable auto upgrade
      --start-upgrader             Install CRON process that checks upgrades
      --stop-upgrader              Removes CRON process that checks upgrades
      --insecure-http-parser       Disables the strict checks
      --new_proxy_port                                          [default: 33335]
      --proxy_country                                              [default: ""]
      --resolve_proxies_interval                                [default: 10000]
      --info                                                    [default: false]
      --av_server                                               [default: false]
      --cn                                                      [default: false]
```

### Docker

'Docker' 이미지는 여기에서 찾을 수 있습니다: [https://hub.docker.com/r/luminati/luminati-proxy/](https://hub.docker.com/r/luminati/luminati-proxy/)

```sh
docker pull luminati/luminati-proxy

docker run luminati/luminati-proxy

docker run luminati/luminati-proxy pmgr --version
```

### SSL リクエ스트

-ssl 파라미터는 SSL analyzing을 위한 것이며, HTTPS リクエ스트는 이를 사용하지 않아도 실행할 수 있습니다.

## 도움말

자주 묻는 질문 [FAQ](https://help.brightdata.com/hc/en-us/sections/12571042542737-Proxy-Manager)

Bright Data FAQ에서 해결 방법을 찾을 수 없다면, [github 에서 질문](https://github.com/luminati-io/luminati-proxy/issues)하실 수 있습니다.

또는 [support@brightdata.com](mailto:support@brightdata.com)로 문의하십시오.

## REST API

API 설명 문서는 앱에서 확인할 수 있습니다.

자세한 설명은 [여기](https://help.brightdata.com/hc/en-us/articles/13595498290065-API)에서 확인할 수 있습니다.

## Node.js API

Proxy Manager는 Node.js 애플리케이션에 필요한 라이브러리로 사용할 수 있으며, 독립적으로 Node.js를 실행해야 하는 필요성을 없애줍니다.

API는 [Promises](https://www.promisejs.org/) 및 [Generators](https://www.promisejs.org/generators/)를 지원합니다. 내부적으로는 [request module](https://github.com/request/request)을 사용하며, 해당 모듈의 모든 기능을 지원합니다.

### Promises
```js
'use strict';
const Server = require('luminati-proxy').Server;

const proxy = new Server({
    customer: 'CUSTOMER', // your customer name
    password: 'PASSWORD', // your password
    zone: 'gen', // zone to use
});
proxy.on('response', res=>console.log('Response:', res));
proxy.listen(0, '127.0.0.1').then(()=>new Promise((resolve, reject)=>{
    proxy.request('http://geo.brdtest.com/mygeo.json', (err, res)=>{
        if (err)
            return reject(err);
        resolve(res);
    });
})).then(res=>{
    console.log('Result:', res.statusCode, res.body);
}, err=>{
    console.log('Error:', err);
}).then(()=>proxy.stop());
```

### Generators
```js
'use strict';
const etask = require('./util/etask.js');
const Server = require('luminati-proxy').Server;

etask(function*(){
    const proxy = new Server({
        customer: 'CUSTOMER', // your customer name
        password: 'PASSWORD', // your password
        zone: 'gen', // zone to use
    });
    yield proxy.listen(0, '127.0.0.1'); // port and ip to listen to
    let res = yield etask.nfn_apply(proxy, '.request',
        ['http://geo.brdtest.com/mygeo.json']);
    console.log('Result:', res.statusCode, res.body);
    yield proxy.stop();
});
```