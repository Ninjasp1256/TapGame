using UnityEngine;
using UnityEngine.UI;
using UnityEngine.SceneManagement;

public class TapGame : MonoBehaviour
{
    public Text scoreText;
    public Text timerText;
    public Button restartButton;  // リスタートボタン
    private int score = 0;
    private float timeLeft = 10f;
    private bool gameOver = false;

    void Start()
    {
        UpdateScoreText();
        UpdateTimerText();
        restartButton.gameObject.SetActive(false);  // ゲーム開始時は非表示
    }

    void Update()
    {
        if (!gameOver)
        {
            if (timeLeft > 0)
            {
                timeLeft -= Time.deltaTime;
                UpdateTimerText();

                if (Input.GetMouseButtonDown(0))  // 画面タップ
                {
                    score++;
                    UpdateScoreText();
                }
            }
            else
            {
                GameOver();
            }
        }
    }

    void UpdateScoreText()
    {
        scoreText.text = "Score: " + score;
    }

    void UpdateTimerText()
    {
        timerText.text = "Time: " + Mathf.Ceil(timeLeft);
    }

    void GameOver()
    {
        gameOver = true;
        restartButton.gameObject.SetActive(true);
    }

    public void RestartGame()
    {
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }
}
