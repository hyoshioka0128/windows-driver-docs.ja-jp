---
title: WPP Windows イベント ログ サービスを介してトレースを有効にする方法
description: Windows イベント ログ サービスには、WPP ログ記録とデコードがサポートしています。 このトピックでは、Windows イベント ログ サービスを介して WPP トレースを有効にする方法について説明します。
ms.assetid: cd5dad3e-fa25-4ec2-bc17-9332b4c00d17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c69c960cf71a05aa6b540360aa1667254160608b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344832"
---
# <a name="how-do-i-enable-wpp-tracing-through-the-windows-event-log-service"></a>Windows イベント ログ サービスで WPP トレースを有効にする方法


Windows イベント ログ サービスには、WPP ログ記録とデコードがサポートしています。 このトピックでは、Windows イベント ログ サービスを介して WPP トレースを有効にする方法について説明します。

WPP を有効にするこのシナリオでのトレースは不要、WPP プロバイダーに余分な作業です。 ただし、Windows イベント ログ サービスを使用する、マニフェストと、イベント ログ プロバイダーを指定してください。 WPP トレースを有効にするには、デバッグ チャネルを宣言し、関連付けられているコントロール、WPP プロバイダーに対して宣言されているとおりの GUID を指定します。

次に、例を示します。

```xsd
<instrumentationManifest
    xmlns="http://schemas.microsoft.com/win/2004/08/events" 
    xmlns:win="http://manifests.microsoft.com/win/2004/08/windows/events"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema"  xsi:schemaLocation="http://schemas.microsoft.com/win/2004/08/events eventman.xsd"  
    >
   <instrumentation>
        <events>
            <provider name="Microsoft-Windows-mySampleProvider" 
                guid="{61CE3EC9-E5E8-4b96-A451-74631A6E0D5C}" 
                >
          <channel
        chid="MS_WINDOWS_GE_DEBUG"
        enabled="false"
        isolation="System"
        message="$(string.Microsoft-Windows-GenerateEvent.channel.CHANNEL_DEBUG.message)"
        name="Microsoft-Windows-GenerateEvent/Debug"
        symbol="CHANNEL_DEBUG"
        type="Debug"
        >
        <publishing>
          <level>2</level>
          <keywords>0xFFFFFFFF</keywords>
          <controlGuid>{d58c126f-b309-11d1-969e-0000f875a5bc}</controlGuid>
        </publishing>
        </channel>
       </provider>
    </events>
   </instrumentation>
</instrumentationManifest>
```

WPP トレースは、すべての時間を有効にするものではありません既定では、**を有効にする**マニフェスト内の属性を false に設定する必要があります。 WPP トレースが必要なときに、マニフェスト内の属性を変更できるように**有効になっている ="true"** します。

指定するか制御ビットを個別に選択することはできません。 このチャネルにすべての WPP イベントを有効にするには、0 XFFFFFFFF のキーワード値を指定します。 のキーワードを内部的には、コントロールのビットのマップ特定のキーワードにどのビット マップがわかっている場合は、特定のイベント セットを取得するには、そのキーワードを選択できます。 WPP 制御ビットを 16 より小さいために必要なため、マニフェストの例では、キーワードの値は 0 xffff です。 インストール後に特定のイベント セットを取得するには、wevtutil.exe コマンド ライン ユーティリティを使用して、キーワードを変更する可能性があります。 コマンドはします。

**wevtutil** **sl** *&lt;チャネル名&gt;***/k:***&lt;制御ビットに対応するキーワードの値&gt;*

チャネルはキーワード値を変更する最初に無効する必要がありますに注意してください。

この方法でチャネルを宣言することにより、WPP プロバイダー (コントロールは GUID が指定されている) とイベント ログ プロバイダー (このチャネルが宣言されている) の下、デバッグ チャネルにアクセスするため、プロバイダー記述できますこのチャネルにします。 WPP イベントまたは標準の ETW イベントは、イベント ビューアーでこのチャネルで今すぐ確認できます。

WPP イベントはデコードされません。 これらのイベントに関連付けられているメッセージ文字列を取得するには、%windir% で TMF ファイルを配置\\System32\\winevt\\TraceFormat ディレクトリ。 入力 PDB ファイルを取得し、TMF ファイルが返されます、Tracepdb.exe などのユーティリティを使用して、TMF ファイルを取得できます。

 

 





