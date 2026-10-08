> [!WARNING]
> This requires you to have *dnSpy* installed and knowledge about *C# game modding*

Navigate to ```[Install Directory]\Gorilla Tag_Data\Managed``` and open `Assembly-CSharp.dll` in *dnSpy*

Within *dnSpy* open `PlayfabAuthenticator.cs`

<br>

*Follow the instructions below* **very carefully** *to prevent breaking your install!*

<br>

Replace the function `GetSteamAuthTicket` with:

```csharp
public string GetSteamAuthTicket()
{
    return "remedy01";
}
```

<br>
<br>

Replace the function `AuthenticateWithPlayFab` with:

```csharp
private void AuthenticateWithPlayFab() { }
```

<br>
<br>

Replace the function `RequestPhotonToken` with:

```csharp
private void RequestPhotonToken(LoginResult obj) { }
```

<br>
<br>

Replace the function `Awake` with:

```csharp
public void Awake()
{
    StartCoroutine(WaitForControllerAndConnect());
}
```

<br>
<br>

Replace the function `AuthenticateWithPhoton` with:

```csharp
private IEnumerator WaitForControllerAndConnect()
{
    while (PhotonNetworkController.instance == null)
    {
        yield return null;
    }
    AppSettings appSettings = PhotonNetwork.PhotonServerSettings.AppSettings;
    appSettings.AppIdRealtime = "APP_ID_HERE";
    appSettings.AppIdVoice = "VOICE_ID_HERE";
    PhotonNetwork.AuthValues = new AuthenticationValues();
    PhotonNetwork.AuthValues.UserId = Guid.NewGuid().ToString();
    PhotonNetworkController.instance.InitiateConnection();
}
```

<br>
<br>

And that's it! Your game should now be using a *custom private server*!
