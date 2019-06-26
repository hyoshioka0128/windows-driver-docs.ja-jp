---
title: 複数のオーディオ サブデバイス
description: 複数のオーディオ サブデバイス
ms.assetid: 1654a2b3-7bec-4438-8cb5-b3136c8e66cc
keywords:
- WDK、サブデバイス多機能オーディオ デバイス
- サブデバイス WDK の複数のオーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a22d039208e639ea72cadfccb9f88b94c3c91459
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363207"
---
# <a name="multiple-audio-subdevices"></a>複数のオーディオ サブデバイス


## <span id="multiple_audio_subdevices"></span><span id="MULTIPLE_AUDIO_SUBDEVICES"></span>


多機能デバイスには、2 つ以上のオーディオ サブデバイスを含めることができます。 たとえば、アダプターのドライバーは 8 チャネル オーディオ デバイスの 4 つのステレオ チャネルとしてシステムに公開するを許可する可能性があります。 この方法で複数のサブデバイスを公開するアダプタのドライバを記述する場合は、ドライバーに、サブデバイスに関する情報を組み込む必要があります[スタートアップ シーケンス](startup-sequence.md)と INF ファイル。

最初に、アダプターのドライバーは、スタートアップ時にポート/ミニポート ドライバーのペアの別のインスタンスとして各ステレオ サブデバイスを公開する必要があります。 Microsoft Windows Driver Kit (WDK) の実装にあるサンプル アダプターのいくつか、`InstallSubdevice`関数を作成し、システム ポート ドライバー、ミニポート ドライバーでは、このペアにバインドされるリソースのセットで構成されるサブデバイスを登録します。 起動中に、ドライバーを呼び出す必要があります、`InstallSubdevice`各ステレオ サブデバイスの 1 回関数をポート/ミニポート ドライバーのペアごとに一意の名前を指定します。

さらに、このペアに割り当てた一意の名前は、ドライバーの INF ファイルで指定した KSNAME 文字列に一致する必要があります。 たとえば、ドライバーに割り当てる可能性が"Wave1"や"Wave2"の名前サブデバイスの 2 つ起動時に、次に示すよう。

```inf
  InstallSubdevice(..., "Wave1",...);
  InstallSubdevice(..., "Wave2",...);
```

この場合、同じ名前は、INF ファイルで表示する必要があります。

```inf
  KSNAME_Wave1="Wave1"
  KSNAME_Wave2="Wave2"
```

INF ファイルには、これらの名前を含むインターフェイスを追加する必要があります。

```inf
  AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave1%,Test.Interface.Wave1
  AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave2%,Test.Interface.Wave2
```

INF ファイルを作成する必要があります**AddReg**セクション (を参照してください[ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)) これらのインターフェイスに関する情報をレジストリに追加するには。

```inf
  [Test.Interface.Wave1]
  AddReg=Test.I.Wave1.AddReg

  [Test.Interface.Wave2]
  AddReg=Test.I.Wave2.AddReg
```

**AddReg**のセクションでは、各サブデバイスのレジストリ エントリも指定する必要があります。

```inf
  [Test.I.Wave1.AddReg]
  HKR,,CLSID,,%Proxy.CLSID%
  HKR,,FriendlyName,,%Test.Wave1.szName%

  [Test.I.Wave2.AddReg]
  HKR,,CLSID,,%Proxy.CLSID%
  HKR,,FriendlyName,,%Test.Wave2.szName%
```

最後に、INF ファイルでは、これらサブデバイスのフレンドリ名を定義する必要があります。

```inf
  Test.Wave1.szName="Punch"
  Test.Wave2.szName="Judy"
```

サブデバイスを識別するためにオーディオ コントロール パネルの フレンドリ名が表示されます。

 

 




