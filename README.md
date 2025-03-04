https://www.youtube.com/watch?v=ubcPWoRY2KE

__Feature1 외곽선 추출, 외곽선 갯수 파악.__

findContours함수 이용, 이미지에 그려진 숫자의 외곽선 갯수를 파악

외곽선의 갯수가 1개일시 숫자 1, 2, 3, 4, 5, 7 중 하나로 추측 가능

외곽선의 갯수가 2개일시 숫자 0, 4, 6, 9 중 하나로 추측 가능

외곽선의 갯수가 3개일시 숫자 8로 추측 가능

__Feature2 외곽선의 무게중심 파악.__

Feature1에서 구한 외곽선과 connectedComponentsWithStats 함수 이용, 도심부 추출, 각 외곽선의 도심을 파악 

외곽선이 2개, 즉 무게중심이 2개일 경우 각 무게중심의 y좌표 차이를 분석, 

외부 외곽선 무게중심의 y좌표가 내부 외곽선 무게중심의 y좌표보다 낮을 경우(외부 외곽선 무게중심이 내부 외곽선 무게중심보다 위에 있을 경우) 숫자 6으로 추측 가능

외부 외곽선 무게중심의 y좌표가 내부 외곽선 무게중심의 y좌표보다 높을 경우(외부 외곽선 무게중심이 내부 외곽선 무게중심보다 아래에 있을 경우) 숫자 4, 9 중 하나로 추측 가능

외부 외곽선 무게중심의 y좌표와 내부 외곽선 무게중심의 y좌표 차이가 미세할 경우(외부 외곽선 무게중심과 내부 외곽선 무게중심이 매우 근접할 경우) 숫자 0으로 추측가능

__Feature3 숫자의 가로, 세로 비율 파악.__

boundingRect, minAreaRect 함수 이용, 외곽선이 1개인 숫자의 경우 숫자를 감싸는 바운딩박스 생성

바운딩박스의 가로길이(width), 세로길이(height)를 파악한 이후 가로길이/세로길이 나눗셈 연산 width/height 값이 비정상적으로 높을 경우, 가로길이가 매우 짧은 일직선 형태의 숫자 1로 추측 가능

__Feature4 숫자에 특정 방향의 선을 그어 접촉하는 면적의 수 확인.__

Feature3 에서 생성한 바운딩박스와 addWeighted 함수 이용, 숫자 이미지의 픽셀값을 낮춘 뒤 선 이미지의 픽셀값을 더한 이후 이진화, 라인과 숫자가 겹친 부분만 남는 원리

1. 숫자의 중앙보다 약간 윗부분에 가로선을 그음. Feature1, 2, 3에서 분석하지 못한 외곽선이 1개인 수 2, 3, 4, 5, 7 중 가로선을 그었을 경우 2개의 면적에 닿는 수는 4, 7 
우측상단 - 좌측하단으로 이어지는 대각선을 그음. 4, 7중 대각선에 검출되는 면적이 1개인 수는 7, 검출되는 면적이 2개인 수는 4로 추측

2-1. 1-1에서 그은 가로선에 1개의 면적이 검출되는 수는 2, 3, 5, 7
세로선을 그음. 2, 3, 5, 7중 세로선에 1개의 면적이 검출되는 수는 7로 추측 

2-2. 세로선에 2개의 면적이 검출되는 수는 모폴로지 연산된 2와 7 
우측상단 - 좌측하단으로 이어지는 대각선을 그음. 대각선에 1개의 면적이 검출되면 7, 2개의 면적이 검출되면 2로 추측 

2-3. 세로선에 3개의 면적이 검출되는 수는 모폴로지 연산이 안된 2, 3, 5 
우측상단 - 좌측하단으로 이어지는 대각선을 그음. 대각선에 2개의 면적이 검출되면 2로 추측

3. 2-3에서 그은 우측상단 - 좌측하단 대각선에 3개의 면적이 검출되는 수는 3, 5 
중앙상단 - 좌측중단으로 이어지는 대각선을 그음. 대각선에 1개의 면적이 검출되면 3, 2개의 면적이 검출되면 5로 추측 

4. 숫자 Feature3에서 구분하지 못한 외곽선이 2개인 숫자 4, 9의 경우 우측중앙 - 중앙하단 대각선을 그어 대각선에 검출되는 면적이 1개면 9, 2개면 4로 추측 
