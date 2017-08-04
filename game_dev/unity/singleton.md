### 유니티에서 싱글톤 사용하기
```Csharp
 public class GameManager : MonoBehaviour {

        public static GameManager instance = null;

        void Awake() {

            if (instance == null) {

                instance = this;

            }

            else if (instance != this) {

                Destroy(gameObject);

            }

            DontDestroyOnLoad(gameObject);

        }
 }
```
