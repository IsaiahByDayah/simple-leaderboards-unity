# simple-leaderboards-unity
Unity package for interfacing with simple-leaderboards backend

Version 0.0.1

## Dependencies:
- [JSONObject](https://github.com/mtschoen/JSONObject) ([Asset Store](https://www.assetstore.unity3d.com/en/#!/content/710))

## Usage



```C#
public class Test : MonoBehaviour {

	private SimpleLeaderboardsManager lb;

	[SerializeField]
	private string gameTitle; // "UnityTestGame"

	void Start () {
		lb = GetComponent<SimpleLeaderboardsManager>();
	}
	
	void Update () {
		if (lb == null) return;

		// Submit
		if (Input.GetKeyDown(KeyCode.S))
		{
			lb.SubmitScore(gameTitle, 2, "SampleUser", ScoreSubmitted);
		}

		// Retrieve
		if (Input.GetKeyDown(KeyCode.R))
		{
			lb.FetchScoresForGame(gameTitle, HighScores);
		}
	}

	void HighScores(SimpleLeaderboardsScore[] scores)
	{
		Debug.Log("High Scores:");
		for (int i = 0; i < scores.Length; i++)
		{
			SimpleLeaderboardsScore s = scores[i];
			Debug.Log((i+1) + ") " + s.user + " - " + s.value);
		}
	}

	void ScoreSubmitted(SimpleLeaderboardsScore score)
	{
		Debug.Log("New Score:");
		Debug.Log(score.user + " - " + score.value);
	}
}
```
