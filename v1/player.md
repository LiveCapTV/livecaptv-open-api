# LiveCapTV Embedded Player

## URL Convention

- http(s)://www.livecap.tv/s/embed/{video_id}
- http(s)://www.livecap.tv/s/embed/{streamer_name}/{video_id}

## Embed a player using an `<iframe>` tag

Define an `<iframe>` tag in your application in which the `src` URL specifies the content that the player will load as well as any other player parameters you want to set. The `<iframe>` tag's `height` and `width` parameters specify the dimensions of the player.

    <iframe src="https://www.livecap.tv/s/embed/riotgames/uLMjA0PqyDe?autoplay=1" width="640" height="360" frameborder="0"></iframe>

Note that you could append player parameters directly to the end of the URL. Following are player parameters currently supported:

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>autoplay</code></td>
            <td>If set to 1, the video would play automatically once the player has loaded.</td>
        </tr>
        <tr>
            <td><code>enablejsapi</code></td>
            <td>Setting the parameter's value to <b>1</b> enables the player to be controlled via <a href="/v1/iframe_api.md">IFrame API</a> calls. The default value is <b>0</b>, which means that the player cannot be controlled using those APIs.<br/>For more information on the IFrame API and how to use it, see the <a href="/v1/iframe_api.md">IFrame API</a> documentation. </td>
        </tr>
        <tr>
            <td><code>origin</code></td>
            <td>This parameter provides an extra security measure for the <a href="/v1/iframe_api.md">IFrame API</a> and is only supported for IFrame embeds. If you are using the <a href="/v1/iframe_api.md">IFrame API</a>, which means you are setting the enablejsapi parameter value to <b>1</b>, you should always specify your domain as the origin parameter value.</td>
        </tr>
        <tr>
            <td><code>t</code></td>
            <td>This parameter causes the player to begin playing the video at the given number of seconds from the start of the video. The parameter value is a positive integer.</td>
        </tr>
        <tr>
            <td><code>show_player_controls</code></td>
            <td>If set to 0, the controls of video player will be hidden. Note that if the width is less than 700px, the controls will show regardless of this parameter for better mobile page UX. Defaults to 1 (Show)</td>
        </tr>
        <tr>
            <td><code>show_share_controls</code></td>
            <td>If set to 0, the buttons of sharing will be hidden. Defaults to 1 (Show)</td>
        </tr>
        <tr>
            <td><code>enable_chats</code></td>
            <td>If set to 1, users will be able to see Twitch reactions in the embedded player. Defaults to 0 (Disabled)</td>
        </tr>
        <tr>
            <td><code>show_chats</code></td>
            <td>If set to 1, the Twitch reactions panel will be at expanded state when player starts up. This parameter will not take effect if <code>enable_chats</code> is set to 0. Defaults to 0 (Collapsed)</td>
        </tr>
        <tr>
            <td><code>show_chat_controls</code></td>
            <td>If set to 0, the bar which controls whether Twitch reactions panel gets expanded will be hidden. This parameter will not take effect if <code>enable_chats</code> is set to 0. Defaults to 1 (Show)</td>
        </tr>
    </tbody>
</table>
