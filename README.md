# Proxy manager

[![dependencies Status](https://david-dm.org/luminati-io/luminati-proxy/status.svg)](https://david-dm.org/luminati-io/luminati-proxy)
[![devDependencies Status](https://david-dm.org/luminati-io/luminati-proxy/dev-status.svg)](https://david-dm.org/luminati-io/luminati-proxy?type=dev)
[![optionalDependencies Status](https://david-dm.org/luminati-io/luminati-proxy/optional-status.svg)](https://david-dm.org/luminati-io/luminati-proxy?type=optional)

전 세계의 プロキシ로 향하는 트래픽을 가속/압축/로ーテーティング/분산/관리/모니터링/보고/로깅/디버그하기 위해 사용자 측에 배치하는 forward HTTP/HTTPS プロキ시입니다.

Proxy manager를 사용하면 Bright Data レジデンシャルプロキシ IP 또는 Bright Data スタティックプロキシ IP를 구동할 수 있습니다.

이 도구를 사용하려면 [Bright Data](https://brightdata.co.kr/?cam=github-proxy) 계정이 필요합니다.  
이슈 또는 버그는 계정 매니저에게 보고하시거나 [help center](https://brightdata.co.kr/faq#proxy)에서 보고해 주시기 바랍니다.

<em>[中文](https://brightdata.co.kr/static/lpm/README-zh-CN.html)으로 읽기.</em>

## Features
- 높은 확장성
- 더 빠른 응답 시간을 위한 커넥션 풀
- 간단한 웹 인터페이스를 통해 여러 구성을 손쉽게 설정
- 통계
- X リクエスト마다 자동으로 IP 로ーテーティング
- 여러 Super Proxies를 사용한 로드 밸런싱
- SSL 분석(자체 서명 인증서 사용)
- SOCKSv5 プロキ시

### Minimal requirements
- 2GB RAM
- 1 CPU
- 3GB HDD

### Recommended requirements
- 4GB RAM
- 2 CPUs
- 3GB SSD

## Installation

### Windows
[Proxy Manager installer](https://github.com/luminati-io/luminati-proxy/releases/download/v1.597.450/luminati-proxy-manager-v1.597.450-setup.exe)을 다운로드합니다.

### Linux/MacOS - Install script
- 설치를 위해 setup 스크립트를 실행합니다.
```sh
wget -qO- https://brightdata.co.kr/static/lpm/luminati-proxy-latest-setup.sh | bash
```
또는
```sh
curl -L https://brightdata.co.kr/static/lpm/luminati-proxy-latest-setup.sh | bash
```
### Linux/MacOS - Manual install
- Node.js를 설치합니다([nodejs.org](https://nodejs.org/en/download/)).  
  Proxy manager용 Node.js 버전은 최소 14.19.0 이상이어야 하며, 20.12.1 버전보다 오래되면 안 됩니다.
- npm 버전이 최소 6.14.6인지 확인합니다.
  - 아니라면 다음을 실행합니다: `sudo npm install -g npm@6.14.6`
- 터미널 프롬프트에서 Proxy Manager를 설치합니다:
```sh
sudo npm install -g @luminati-io/luminati-proxy
```
- npm 버전이 6보다 높다면 '--legacy-peer-deps' 플래그를 추가해 주시기 바랍니다:
```sh
sudo npm install -g @luminati-io/luminati-proxy --legacy-peer-deps
```
중국에서 Mac/Linux로 Proxy Manager 설치를 시도하는 경우, npm이 허용된 registry로 설치하도록 먼저 다음 명령을 실행해 주시기 바랍니다:
```sh
 npm config set registry https://r.cnpmjs.org/
```
이 명령이 성공적으로 실행된 후 다음을 사용하여 설치합니다:
```sh
sudo npm install -g @luminati-io/luminati-proxy --allow-root
```
### Upgrade
- npm을 사용하여 업그레이드합니다.
```sh
sudo npm install -g @luminati-io/luminati-proxy
```
또는 cli 명령을 사용합니다:
```sh
proxy-manager --upgrade
```

### Specific Version
- 특정 Proxy manager 버전을 설치하려면 [releases](https://github.com/luminati-io/luminati-proxy/releases)에서 버전을 선택합니다.

- 실행합니다(VERSION_NUMBER는 선택한 버전입니다(예: 1.75.355)):
```sh
sudo npm install -g @luminati-io/luminati-proxy@VERSION_NUMBER
```

### Release Notes

각 버전의 변경 사항 목록은 [CHANGELOG.md](CHANGELOG.md)에서 확인할 수 있습니다.

## Usage

### First run
앱을 처음 실행한 후:
```sh
proxy-manager
```
자격 증명을 설정하고 プロキ시를 구성하려면 브라우저에서 앱 admin UI인
[http://127.0.0.1:22999](http://127.0.0.1:22999)로 이동합니다.

### Run as daemon
Proxy manager를 백그라운드에서 실행하려면:
```sh
proxy-manager --daemon
```

### Dropin replacement for existing super-proxies

Proxy Manager에는 기존 super-proxies와 정확히 동일하게 동작하는 "dropin mode"가 포함되어 있습니다. dropin mode로 プロキ시를 실행할 때는, プロキ시를 통해 リクエスト를 보내기 위해 administrative UI에서 로그인할 필요가 없습니다. 대신 각 リクエスト마다 プロキ시 서버에 전달되는 プロキ시 사용자 이름과 비밀번호가 제공됩니다. 이 모드는 기본으로 활성화되어 있으며, 일반 super-proxy에서 Proxy Manager로 마이그레이션할 때 손쉬운 대체 수단으로 사용할 수 있습니다.

Dropin mode는 기본으로 활성화되어 있습니다. dropin プロキ시를 비활성화하려면 `--no-dropin` 플래그를 사용합니다:

```sh
proxy-manager --no-dropin
```

dropin プロキ시를 통해 リクエスト를 만드는 API에 대한 전체 문서는 <a href="https://brightdata.co.kr/cp/zones/proxy_examples?type=api&group=active">Bright Data 계정의
API Example 페이지</a>를 참조하시기 바랍니다.

### Complete list of command line options

```sh
proxy-manager --help
Usage:
  proxy-manager [options] config1 config2 ...

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

Docker 이미지는 [https://hub.docker.com/r/luminati/luminati-proxy/](https://hub.docker.com/r/luminati/luminati-proxy/)에서 확인할 수 있습니다.

```sh
docker pull luminati/luminati-proxy

docker run luminati/luminati-proxy proxy-manager

docker run luminati/luminati-proxy proxy-manager --version
```
적절한 포트를 포워딩해야 합니다. Proxy manager는 기본적으로 웹 콘솔과 api에 22999를 사용하고, dropin에는 22225를 사용하며, 첫 번째 구성 가능한 プロキ시에는 24000을 사용합니다.

- cli 옵션으로 docker를 실행하려면 아래 예시를 참고하시기 바랍니다:
```sh
docker run luminati/luminati-proxy proxy-manager --www_whitelist_ips "172.17.0.1" --ssl true
```
이 실행에 더 많은 옵션을 추가할 수 있습니다.

#### Docker with predefined config file
lpm의 config file을 사용하려면 docker volumes를 사용할 수 있습니다:
https://docs.docker.com/storage/volumes/

다음 지침을 따르면 특정 config file로 docker를 실행할 수 있습니다:

- 볼륨 생성
```sh
docker volume create lpm-vol
```
- 최근 생성된 볼륨을 Inspect합니다.
```sh
docker inspect lpm-vol
```
다음과 유사한 출력이 표시되어야 합니다:
```sh
  [
    {
        "CreatedAt": "2018-02-01T12:59:58+02:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/lpm-vol/_data",
        "Name": "lpm-vol",
        "Options": {},
        "Scope": "local"
    }
  ]
```
- mountpoint 경로 /var/lib/docker/volumes/lpm-vol/_data 를 가져와 다음을 실행합니다.
```sh
cd /var/lib/docker/volumes/lpm-vol/_data
```
- 이 디렉터리에 .luminati.json을 넣습니다(여기에는 컨테이너가 생성하는 logs 및 기타 파일도 저장됩니다).
- docker 이미지를 실행하고 이 볼륨을 attach합니다:
```sh
  docker run --rm --name 'lpm1' --mount source=lpm-vol,target=/root
"luminati/luminati-proxy" proxy-manager
```

### SSL Requests

--ssl パラメータ는 SSL 분석을 위한 것이며, HTTPS リクエスト는 이를 사용하지 않아도 보낼 수 있습니다.

## Help

FAQ는 Bright Data
[FAQ](https://help.brightdata.com/hc/en-us/sections/12571042542737-Proxy-Manager)에서 확인할 수 있습니다.

그곳에서 답을 찾지 못하셨다면, 편하게
[issue on github](issues)를 열어 주시기 바랍니다.

또는 [support@brightdata.com](mailto:support@brightdata.com)으로 문의하시기 바랍니다.

## REST API

API의 동작 문서는 앱 내부에서 확인할 수 있습니다.

API는 Bright Data에서 [here](https://help.brightdata.com/hc/en-us/articles/13595498290065-API)에서도 확인할 수 있습니다.