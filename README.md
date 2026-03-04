name: Build APK v3
on: push
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17

      - name: Make gradlew executable
        run: chmod +x gradlew

      - name: Build APK
        run: ./gradlew assembleDebug

      - name: Rename APK
        run: cp app/build/outputs/apk/debug/app-debug.apk TicTacToe.apk

      - name: Upload APK
        uses: actions/upload-artifact@v4
        with:
          name: TicTacToe
          path: TicTacToe.apk
          retention-days: 7
