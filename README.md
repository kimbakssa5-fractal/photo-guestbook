# 📸 포토 방명록 (재설계 버전)

`spider-kiosk`의 포토 방명록을 **깔끔한 UI로 새로 설계**한 버전.
디자인 컨셉: **`01_fractal canvas`의 fractal_4 디자인** — 상단 다크 그라데이션 헤더(검정→흰색) + 중앙 빨강(#fd0136) 역삼각 탭 + `|`로 구분된 흰 텍스트 메뉴 + 다크 트랙·흰 손잡이 슬라이더, 흰색 작업영역.

## 흐름

시작 → 카메라(3초 촬영) → 꾸미기(펜·스티커·글자·프레임) → QR 전송

| 파일 | 설명 |
|---|---|
| `index.html` | 포토 방명록 본체 (단일 파일, 4개 화면) |
| `admin.html` | 기록 관리 (전체 보기/다운로드/삭제) |
| `guestbook-store.js` | 저장소 — IndexedDB(원본·무제한) + Firebase 동기화(선택) |
| `firebase-config.js` | Firebase 연동 설정(선택, 미설정이어도 로컬 저장 정상) |
| `qrcode.min.js` | QR 생성 |
| `assets/menu.jpg` | 시작화면 히어로 이미지 (`09_photo sticker/menu` 원본 리사이즈) |
| `stickers/lip_NN.png` | 입술 스티커 12종 — `09_photo sticker/item` 시트에서 흰 배경 제거·개별 추출한 투명 PNG |

## 기존 버전 대비 정리한 것

- 화면마다 **주요 동작 1개**만 크게, 도구는 탭형 하단 툴바로 정돈
- 제거: BGM 파일 로더, 커스텀 셔터 로더, 보관기간 순환 버튼(72h 기본 고정), 4종 프레임·할로윈 이모지 떼, 거미줄 펜·거미줄 프레임 등 거미 테마
- 펜: 일반 펜(색·굵기·지우개) / 프레임: 없음·흰 테두리
- 스티커: 이모지 → **포토부스 입술 스티커 이미지**(드래그·크기조절)로 교체
- 시작화면: 텍스트 워드마크 → "Photo Guestbook" 무드 이미지 히어로
- 검증된 저장·업로드 로직(IndexedDB / litterbox 72h / tmpfiles 60분 / Firebase Storage)은 그대로 재사용

## 실행

카메라(`getUserMedia`)는 **https 또는 localhost**에서만 동작.
파일을 직접 열지 말고 로컬 서버(`npx serve .`)나 GitHub Pages로 띄울 것.
