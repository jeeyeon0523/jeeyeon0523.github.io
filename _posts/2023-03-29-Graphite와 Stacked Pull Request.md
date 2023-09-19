---
layout: post
title: Graphite로 Stacked Pull Request 하는 법
subtitle: 모던 코드리뷰 나도 해보기
categories: study
tags: [github, graphite, pull request]
---

## Stacked Changes 란?

개념은 나중에 작성!

작년에 에이든님이 공유해주신 인프콘 발표 자료가 설명이 잘 되어 있는 듯 하다. -> https://www.slideshare.net/JiyeonSeo2/pull-requests-vs-stacked-changes

기존에 1스토리-> 1PR이었다면, 1스토리-> 다수의 stack PR이 가능해짐.

## Github에서 Graphite 사용하기

### What is Graphite

- 모던 코드리뷰를 도와주는 툴?, 앱?, 서비스? 어쨌든 그러한 것임.
- 이런 기능을 하는 서비스들이 많이 있지만 현재 살아남은 대세.
- 그럼에도 불구하고 아직은 베타 버전 (2023.03 기준)
- 코드 변경을 stack 단위로 관리하여 작은 크기의 리뷰와 머지를 가능하게함
- github에 해당 앱을 Import 하여 사용할 수 있음.
- 슬랙 메시지, AI PR description summarize 등 다양한 편의 기능 제공

### How To Use Graphite

[공식 다큐먼트 퀵스타트](https://graphite.dev/docs/graphite-quick-start) 페이지를 따라하며 stack과 stacked PR의 개념을 익힐 수 있다.
(특별한 이슈가 없다면 1시간 컷 가능)

**github 계정과 바로 연결해서 쓸 수 있다**
<img width="575" alt="스크린샷 2023-03-29 오전 12 59 42" src="https://user-images.githubusercontent.com/47856202/228715325-81688e66-7fa9-4f7a-a01e-5dc1256a3251.png">

**slack 채널과 연결도 해줌 (메시지를 어떻게 보내는지 까지는 모름)**
<img width="504" alt="스크린샷 2023-03-29 오전 1 04 42" src="https://user-images.githubusercontent.com/47856202/228715737-1645b6f7-8794-4523-ad33-d8fe3d094a0a.png">

개발환경 세팅은 크게

- graphite를 깃헙 레포에 import
- 로컬 환경에 graphite 설치

이 정도의 스텝으로 나눠서 사용 가능하다.

**main에 edit_readme, edit_readme 아래에 stack과 pr을 생성한 모습**

<img width="522" alt="스크린샷 2023-03-30 오전 12 54 00" src="https://user-images.githubusercontent.com/47856202/228716112-3ae85813-e9a3-43e6-b1f3-463527ee3ffd.png">

**merge1 stack과 하위 stack들을 생성한 모습**

<img width="540" alt="스크린샷 2023-03-30 오전 12 59 57" src="https://user-images.githubusercontent.com/47856202/228716424-7d1533e5-a453-44d7-8104-6e38ac70e100.png">

**graphite 대시보드에서 stack들을 한번에 머지할 수 있음**

<img width="1424" alt="스크린샷 2023-03-29 오후 12 29 04" src="https://user-images.githubusercontent.com/47856202/228716705-2de0e98c-fdb3-4a65-ac4c-cae7442220b6.png">

## 프로젝트에서 사용 가능할까? 장점, 단점, 고려할 점을 뭉뜽그려

- diff가 stack 단위로 보여지니 정말 작은 단위로 리뷰 및 머지가 이뤄질 수 있을 것 같음.
- 대신 그만큼 많아지는 PR 수
- stack branch 마다 파이프라인을 만들 수 있는건지 ~~미지수~~ 되는것 같음! 어떻게 하는지 아직 모를뿐.. + 만들어진다면 자원낭비가 되나? => 파이프라인 운영 정책 필요
- github과 graphite 대시보드 : 두개의 pr 관리 채널이 생김 (장점일지 단점일지 판단 필요)
- stack의 개념, graphite 사용법등 러닝커브 필요 (일단 겉보기에는 얕아보임)
- 소스트리와 같이 gui로 동작시킬 수 있는 툴이 아직 없는 것 같음.
- 기능별, 혹은 코드별 (스프링부트 be의 경우 controller, service 등 단위처럼) stack으로 분리할 수 있는 개발 요건이 명확할 경우에 장점이 부각될 것 같음.
- 위와 비슷한 이야기긴한데, 어떤 기준으로 하나의 스택을 나눌 건지 (작을수록 좋은 것만 같지는 않은데?!) 정책적, 경험적(?) 기준이 필요함.
- 코드리뷰는 하나의 개발문화(?)라고 생각하는 편인데, 새로운 문화를 도입하는 차원에서 우려스러운 면이 있음. 아무도 경험해 본적 없는 길을, 잘 가고 있는지 아닌지 어떻게 알 수 있을까?
