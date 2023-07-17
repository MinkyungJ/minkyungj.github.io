---
layout: post
title: Docker Volume
tags: [DevOps, Docker, Container, Volume]
date: 2023-07-12 15:00 +0800
last_modified_at: 2023-07-12 18:00:00 +0800
categories: Docker
toc: true
---

# Docker Volume을 왜  사용해야 할까요?
도커 컨테이너는 컨테이너마다 기본적으로 독자적인 저장소를 가지고 있습니다. 하나의 이미지로 여러 개의 컨테이너를 생성할 시, 각 컨테이너마다 독립적인 볼륨이 할당됩니다. 또한, 컨테이너가 삭제 될 시, 해당 볼륨 또한 삭제되며, 이때 컨테이너 내부에 저장되는 내부 데이터는 컨테이너가 삭제될 때 같이 삭제됩니다. 

예를 들어, 도커 컨테이너 내부에 min.txt 파일이 저장되어 있습니다. 제가 해당 파일이 들어있는 컨테이너를 삭제하면 컨테이너 내부 볼륨에 존재하는 파일 또한 함께 삭제될 것입니다. 

![Why_use_Volume](https://github.com/MinkyungJ/MinkyungJ.github.io/blob/main/_posts/Why_use_Volume.png?raw=true)

이러한 구조와 같이 컨테이너 내부에 중요한 데이터를 저장하는 것은 안전하지 않은 방법으로 보입니다. 이를 위해, 도커는 데이터의 영속성을 보장하기 위해 여러 방법을 지원하고 있고 이는 도커 볼륨을 사용해야 하는 이유입니다.
도커 볼륨은 영속성을 보장하며 파일 시스템과 컨테이너를 분리하여 관리합니다. 즉 컨테이너를 지웠다가 다시 실행해도 도커 볼륨과 연결한다면 데이터는 그대로 유지된 상태입니다.

# Docker Volume 종류

## 볼륨 (Docker Volume)
- 도커 엔진이 관리하는 디렉터리로, 호스트 파일 시스템의 특정 위치에(/var/lib/docker/volumes/) 저장됩니다. 
- 컨테이너에서 사용하는 데이터를 영구적으로 저장하고 공유할 수 있습니다.
- 가장 권장되며 대중적인 방법으로 도커 명령어를 통해 볼륨을 생성, 관리할 수 있습니다.
- 호스트와 분리되어 있어 데이터의 보안성과 이식성이 높습니다.
- 도커 컨테이너 간 볼륨은 공유될 수 있고, 컨테이너 재시작 시에도 유지됩니다.

![Docker_Volume](https://github.com/MinkyungJ/MinkyungJ.github.io/blob/main/_posts/Docker_Volume.png?raw=true)

## 바인드 마운트 (Host Bind Mount)
- 호스트 파일 시스템의 특정 경로를 컨테이너의 경로에 마운트합니다.
- 호스트와 컨테이너 간에 파일 변경이 서로 반영되며, 동기화됩니다.
- 호스트의 파일 시스템에 직접 접근하기 때문에 빠른 성능을 가지고 있습니다.
- 도커 외부에서도 데이터에 접근할 수 있습니다.
- **단점**
  - 도커의 관리 없이 호스트 디렉터리와 마운트하기 때문에, 컨테이너에 지정된 파일이 아닌 다른 파일 또한 관리할 수 있다는 단점이 존재합니다.
  - 호스트 파일 시스템의 경로를 컨테이너에 노출시키므로 보안에 유의해야 합니다.

![Host_Bind_Mount](https://github.com/MinkyungJ/MinkyungJ.github.io/blob/main/_posts/Host_Bind_Mount.png?raw=true)

## 템프티 마운트 (Tmpfs)
- 리눅스에서 도커를 실행하는 경우에만 사용할 수 있는 기능으로 호스트의 임시 파일 시스템을 컨테이너의 경로에 마운트합니다.
- 볼륨을 메모리에 저장하는 방식을 사용하여 속도는 빠르지만, 컨테이너가 삭제되면 데이터도 함께 삭제됩니다.
- 임시 파일 시스템으로 일시적인 데이터 저장에 적합하며 주로 파일 형태로 저장하면 안되는 민감한 정보를 저장할 때 사용합니다.

![Tmpfs_Mount](https://github.com/MinkyungJ/MinkyungJ.github.io/blob/main/_posts/Tmpfs_Mount.png?raw=true)

# Reference
<https://docs.docker.com/storage/volumes/>