# Flutter CI/CD Pipeline using Github Actions
![Build and Deploy Action](https://github.com/atavci/flutter_ci_cd_pipeline/actions/workflows/flutter-github-action.yml/badge.svg)</br>
A sample project for building Flutter CI/CD Pipeline using Github Actions.

### Pipeline steps:
- Gets Dependencies  🧰</br> 
- Runs tests  🧪</br> 
- Builds an APK package  📦</br>
- Uploads the APK to Github Artifactory  ☁</br>

## Make it your own

### Option 1
- Fork this repository
- Remove the contents of the flutter project folder and clone your own repository.
- Edit .gitmodules file:
```
[submodule "flutter_project"]
	path = flutter_project
	url = <add_your_github_repository_link.git>

```
- Profit.

### Option 2
- Create .github/workflows directory in your project
- Add flutter-github-action.yml from this repository to the created directory.
- Configure your project path on line 13 of the .yml file
```yaml
Name: Flutter Github Action
on: [push]
jobs:
  android_build_and_publish:
    runs-on: ubuntu-latest
    name: Flutter Build
    strategy:
      fail-fast: true
      matrix:
        os: [ubuntu-latest, windows-latest, macOS-latest]
    defaults:
      run:
        working-directory: flutter_project # add your project directory or remove this block to use the root folder
```
- Configure the path for Upload APK step:
```yaml
      - name: Upload APK
        uses: actions/upload-artifact@v1
        with:
          name: flutter_apk
          path: flutter_project/build/app/outputs/flutter-apk/app-release.apk # Configure according to your project path
```
- You are set.

## Some details
* Runs on every push to repository.
* Flutter Project folder is configured to be used a git submodule as the project to be built and deployed.

## Contribution
Feel free to contribute. You can also join a discussion on the issues section.




