
### [문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17687)

<br><br>

### 1. 코드
<br>

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

string solution(int n, int t, int m, int p) {
	string answer = "";

	vector <char> temp_v;
	string temp_s = ""; 

    //temp_s의 크기가 인원수 * 숫자의 갯수만큼 될때까지 반복
	for (int i = 0; temp_s.size() <= t * m; i++) {
					
		int temp_i = i;
		
		do {
			
            /* temp_i % n은 10 이하이면 48을 더해주어 vector <char>인 
            temp_v에 넣어준다. 숫자는 아스키 코드로 48부터 시작이므로*/
			if (temp_i % n < 10) temp_v.push_back(temp_i % n + 48);
			
            /*temp_i % n이 10이상인 경우 55를 더해주어 temp_v에 넣어준다.
            대문자 알파벳이 55부터 이므로 */
			else temp_v.push_back(temp_i % n + 55);

		} while (temp_i /= n);

		for (int j = temp_v.size() - 1; j >= 0; j--) temp_s += temp_v[j];
		temp_v.clear();

	}

	for (int i = p - 1, j = 0; j < t; j++, i += m) {
		answer += temp_s[i];
	}

	return answer;
}
```
<br><br>



