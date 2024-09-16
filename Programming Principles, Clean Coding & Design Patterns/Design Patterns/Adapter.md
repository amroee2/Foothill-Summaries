# Adapter

The Adapter Design Pattern allows objects with incompatible interfaces to collaborate by providing a wrapper that makes one interface compatible with another. It's useful when you have existing classes that are not directly compatible with each other, but you want them to work together without modifying their code.

Assume we have these classes

```csharp
public interface IMediaPlayer
{
    void PlayAudio(string fileName);
}

public class AudioPlayer : IMediaPlayer
{
    public void PlayAudio(string fileName)
    {
        Console.WriteLine($"Playing audio: {fileName}");
    }
}

public class VideoPlayer
{
    public void PlayVideo(string fileName)
    {
        Console.WriteLine($"Playing video: {fileName}");
    }
}

public class MediaClient
{
    private IMediaPlayer _mediaPlayer;

    public MediaClient(IMediaPlayer mediaPlayer)
    {
        _mediaPlayer = mediaPlayer;
    }

    public void PlayMedia(string fileName)
    {
        _mediaPlayer.PlayAudio(fileName);
    }
}
```

We want to the VideoPlayer class to implement the media player, but it can't play an audio, which stops us from implementing it and therefore is not integrated in the MediaClient _mediaPlayer dependency 

Solution for this using an adapter

```csharp
public class VideoPlayerAdapter : IMediaPlayer
{
    private VideoPlayer _videoPlayer;

    public VideoPlayerAdapter(VideoPlayer videoPlayer)
    {
        _videoPlayer = videoPlayer;
    }

    public void PlayAudio(string fileName)
    {
        _videoPlayer.PlayVideo(fileName);
    }
}

class Program
{
    static void Main()
    {
        IMediaPlayer audioPlayer = new AudioPlayer();
        MediaClient audioClient = new MediaClient(audioPlayer);
        audioClient.PlayMedia("song.mp3");

        // Client code using VideoPlayer through the adapter
        VideoPlayer videoPlayer = new VideoPlayer();
        IMediaPlayer videoAdapter = new VideoPlayerAdapter(videoPlayer);
        MediaClient videoClient = new MediaClient(videoAdapter);
        videoClient.PlayMedia("movie.mp4");
    }
}
```
