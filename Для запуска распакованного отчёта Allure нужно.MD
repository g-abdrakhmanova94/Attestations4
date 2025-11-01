1.Создайте файл run-server.bat в папке с распакованным отчетом с содержимым:

  @echo off
  echo Starting Allure Report Server...
  echo Open http://localhost:8000 in your browser
  timeout /t 2
  start http://localhost:8000

  :: Используем встроенный веб-сервер Windows
  powershell -Command "$listener = New-Object System.Net.HttpListener; $listener.Prefixes.Add('http://localhost:8000/'); $listener.Start(); while ($listener.IsListening) { $context = $listener.GetContext(); $path = $context.Request.Url.LocalPath; if ($path -eq '/') { $path = '/index.html' }; $filePath = Join-Path '%CD%' $path.TrimStart('/'); if (Test-Path $filePath -PathType Leaf) { $content = [System.IO.File]::ReadAllBytes($filePath); $context.Response.OutputStream.Write($content, 0, $content.Length) } else { $context.Response.StatusCode = 404 }; $context.Response.Close() }"

2.Запустить этот bat файл двойным кликом, откроется ссылка http://localhost:8000/, в ней откроется мой отчёт Allure