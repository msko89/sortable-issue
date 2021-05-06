## jQuery-ui Sortable Issue

||Note3|Note4|Note5|
|------|---|---|---|
|가로 해상도(px)|1080|1440|1080|
|DPI(디바이스 집적도)|480|640|420|
|디바이스 화면 밀도(DP)|360|360|411.428..|
||1|1|1.14|

cf) px = dp \* ( dpi / 160 )

- jquey.ui.sortable change 기준

1. \_intersectsWithPointer 함수에서 확인.
2. Drag 대상의 offset 위치 + Drag 대상의 click 한 offset 위치, 변경하려는 대상의 위치, sortable items width,height 등으로 계산.
3. Note5의 경우 offset.click.left 값이 다른 디바이스에 비해 큼.
4. offset.click.left의 값은 \_mouseStart 함수에서 설정하는데, event.pageX – offset.left 값으로 설정.(jquery.ui.js 16750 라인 수정)
5. event.pageX 값을 DP 값 비율로 맞추기 위해, Note5인 경우 event.pageX 값을 12%(1.14 값을 1로줄이기 위해서) 감소 시킴.(jquery.ui.js 17973 라인 수정)
6. 정상적으로 동작함을 확인.
7. 해당 이슈는 n x n grid 일 경우에만 발생(1 x n 일 경우에는 문제 발생하지 않을 거라 생각)
