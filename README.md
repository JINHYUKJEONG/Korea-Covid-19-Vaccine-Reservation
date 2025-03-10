# Korea-Covid-19-Vaccine-Reservation [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[코로나 잔여 백신 예약 매크로](https://github.com/SJang1/korea-covid-19-remaining-vaccine-macro) 1.0.24 의 커스텀 빌드입니다.

지정한 좌표 내 대기중인 병원에서 잔여 백신이 확인될 시 설정한 백신 종류로 예약을 시도합니다.

## 변경 사항
### 속도 향상
- **request delay가 없습니다. 주의해주세요.** (변경 전: 200ms)
- 예약 실패 시의 delay가 없습니다. (변경 전: 80ms)
- 대기 중인 병원 리스트는 `p` 키를 누를 시에만 출력됩니다. (변경 전: 항상 출력)
- 잔여 백신 발견 시, 우선 예약 시도 후 발견 안내문을 출력합니다. (변경 전: 안내문 출력 후 예약 시도)
- 로직 간소화를 위해 ANY 옵션을 지원하지 않습니다.
- 잔여 백신이 있는 병원이 여러 곳일 때, 한 곳의 예약이 실패해도 바로 다음 병원에 예약을 시도합니다. (변경 전: 다음 병원 스킵)

### 코드 정리
- mp3가 재생되지 않아 경로를 프로그램 경로로 수정했습니다. 하단의 **주의 사항**을 참고해주세요.
- 잔여 백신 존재 병원이 None인지 검사하는 구문이 제거되었습니다.
- `find_vaccine`에서의 `while` 문을 `break` 하지 않고 바로 `try_reservation`을 호출합니다.
- `clear`, `resource_path` 함수가 제거되었습니다.

### UI
- 실행 시 커스텀 빌드 안내용 배너가 출력됩니다.
```
* * * * * * * * * * * * * * * * * * *
*                                   *
*        1.0.24 CUSTOM BUILD        *
*            by Queue_ri            *
*                                   *
* * * * * * * * * * * * * * * * * * *
```

## 이용 방법
1. Chrome 브라우저를 실행합니다.
2. [카카오 계정 로그인 페이지](https://accounts.kakao.com/login?continue=https%3A%2F%2Fvaccine-map.kakao.com%2Fmap2%3Fv%3D1)에서 로그인합니다. [(로그인 시 주의사항)](https://github.com/SJang1/korea-covid-19-remaining-vaccine-macro/issues/82)
3. [카카오 백신 맵](https://vaccine-map.kakao.com/map2?v=1)으로 위치 지정 후 `개발자도구` - `Network` 탭에서 좌표 값을 찾습니다.
4. `pyinstaller`로 `cb.py`를 빌드합니다.
5. 백신 코드와 좌표가 입력되면 자동 예약을 시도합니다. 이전 설정(`config.ini`)이 있다면 해당 설정을 재사용할 수 있습니다.
6. 예약 성공 시 빵빠레 소리와 함께 예약이 성공했음이 안내됩니다.

## 주의 사항
- **프로그램을 동시에 너무 많이 실행하면 카카오 계정이 정지될 수 있습니다.**
- 오류가 발생하거나 예약에 성공한 경우 프로그램이 자동 종료됩니다.
- 예약 시도가 반드시 성공한다는 보장은 없습니다.
- `exe` 빌드 시 `mp3` 파일과 같은 경로에 위치해야 합니다.
- tmux, screen과 같은 터미널 멀티플렉싱 프로그램이 자동으로 실행되지 않아야 합니다.
- 바이러스가 탐지될 시 이는 오진(false positive)입니다.

## Disclaimer
- 본 프로그램은 매크로를 이용한 백신 예약을 유도하는 내용이 아니며, 해당 프로그램을 사용함으로서 생기는 책임은 모두 이용자 본인에게 있습니다.
