




usecase
https://github.com/google/iosched/blob/b0c6384b4b26efdac16142b8e85b1d8859053a48/shared/src/main/java/com/google/samples/apps/iosched/shared/domain/CoroutineUseCase.kt
https://github.com/google/iosched/blob/b0c6384b4b26efdac16142b8e85b1d8859053a48/shared/src/main/java/com/google/samples/apps/iosched/shared/domain/settings/SetThemeUseCase.kt



flow usecase
https://github.com/google/iosched/blob/b0c6384b4b26efdac16142b8e85b1d8859053a48/shared/src/main/java/com/google/samples/apps/iosched/shared/domain/FlowUseCase.kt


viewmodel
https://github.com/google/iosched/blob/b0c6384b4b26efdac16142b8e85b1d8859053a48/mobile/src/main/java/com/google/samples/apps/iosched/ui/settings/SettingsViewModel.kt


data store
https://github.com/google/iosched/blob/b0c6384b4b26efdac16142b8e85b1d8859053a48/shared/src/main/java/com/google/samples/apps/iosched/shared/data/prefs/PreferenceStorage.kt


```
val text : Flow<String> = context.dataStore.data 
.catch { exception -> 
	if (exception is IOException) { 
		emit(emptyPreferences()) 
	} else { throw exception } 
} 
.map {preferences -> preferences[stringKey] ?: "" }
````
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM0NTAxNDQ1OF19
-->