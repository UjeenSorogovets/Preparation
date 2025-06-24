# Async & Concurrency

[⬅️ Back to Table of Contents](README.md)

### 40. What does ConfigureAwait(false) actually do?

**Answer:** `ConfigureAwait(false)` tells the awaited task **not** to capture the current `SynchronizationContext` (or the current thread's context) when resuming after `await`. This avoids deadlocks in UI/ASP.NET apps and improves throughput in library code because the continuation can resume on any thread pool thread instead of the original context (UI thread or request context).

```csharp
// Library code
public async Task<string> DownloadAsync(string url)
{
    using var client = new HttpClient();
    var data = await client.GetStringAsync(url).ConfigureAwait(false);
    // Continue on thread-pool, not UI thread
    return data;
}
```

Do **not** use `ConfigureAwait(false)` in application/UI layers where you need to update UI controls afterwards.

### 41. What are the benefits of IAsyncEnumerable<T> and await foreach?

**Answer:** `IAsyncEnumerable<T>` represents an asynchronous stream—data produced over time. Benefits:
- **Incremental processing:** Start consuming items before the entire collection is available.
- **Reduced memory:** No need to buffer entire result sets (e.g., database rows, network packets).
- **Back-pressure:** Consumer `await foreach` naturally awaits producer.
- **Unified syntax:** Similar to regular `IEnumerable<T>` with `yield return`.

```csharp
public async IAsyncEnumerable<int> GenerateAsync()
{
    for (int i = 0; i < 3; i++)
    {
        await Task.Delay(500); // Simulate async work
        yield return i;
    }
}

await foreach (var item in GenerateAsync())
{
    Console.WriteLine(item);
}
```

### 42. Why was IAsyncDisposable added and how does it work?

**Answer:** Some resources (network sockets, file handles) need **asynchronous cleanup**—e.g., flushing buffers or informing remote servers. `IAsyncDisposable` provides an `ValueTask DisposeAsync()` method that can be awaited. The `await using` statement ensures deterministic, async disposal.

```csharp
public class AsyncResource : IAsyncDisposable
{
    private readonly Stream _stream;

    public AsyncResource(Stream stream) => _stream = stream;

    public async ValueTask DisposeAsync()
    {
        await _stream.FlushAsync();
        _stream.Dispose();
    }
}

await using var res = new AsyncResource(File.Create("data.bin"));
// Use resource
``` 