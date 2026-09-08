# .NET Guide

## Run App

### Steps to Run Application Locally

As the application would be deployed:

1. **Publish local package**
   - Go to publish folder
   - Open command prompt from the directory

2. **Set environment variables**
   ```powershell
   set ASPNETCORE_ENVIRONMENT=Development
   set IsDevelopmentMode=true
   ```

3. **Run the application**
   ```bash
   dotnet app.dll --urls http://localhost:3000
   ```
