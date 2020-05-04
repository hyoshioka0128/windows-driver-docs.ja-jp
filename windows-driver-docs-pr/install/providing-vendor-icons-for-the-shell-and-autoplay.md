---
title: デバイス用アイコンの提供
description: デバイス用アイコンの提供
ms.assetid: 2e3afbf6-57f6-4b83-b10a-c33d9b1c1731
keywords:
- 自動再生アイコン WDK
- カスタムアイコン WDK デバイスのインストール
- ベンダアイコン WDK
- アイコン WDK シェル
- シェルアイコン WDK
- メディアに挿入されたアイコン WDK
- メディアが挿入されていないアイコン WDK
- アイコン WDK 自動再生
- アイコンファイルをコピーする
ms.date: 04/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: 60effd65f171336e37e1f0c5d18eb7ca27c95bd7
ms.sourcegitcommit: ea42499bb6c405abaa8b1093afa741cd3910da66
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82619778"
---
# <a name="providing-icons-for-a-device"></a>デバイス用アイコンの提供

このトピックでは、ドライバーの INF ファイルでデバイスを参照することによって、デバイスのカスタムアイコンを指定する方法について説明します。 必要に応じて、デバイスマネージャー、Windows エクスプローラー、またはその両方に表示されるアイコンを指定できます。

## <a name="adding-icons-for-device-manager"></a>デバイスマネージャーのアイコンの追加

DLL にカスタムアイコンを埋め込むか、スタンドアロンの .ico ファイルを指定することができます。 ドライバーが既に DLL ファイルである場合は、追加のファイルをコピーする必要がないため、最初のオプションが最も簡単なオプションです。

DLL にアイコンを埋め込むには、次のようなエントリを使用します。

```inf
[<DDInstall>]
AddProperty = DeviceIconProperty

[DeviceIconProperty]
DeviceIcon,,,,"%13%\UmdfDriver.dll,-100"
```

上の例では、DIRID 13 を使用して、ファイルをドライバーストアにコピーします。これにより、他の場所にコピーする必要がなくなります。 エントリはの形式`<Resource.dll>,-<IconResourceID>`に従っているため、100は DLL のリソーステーブル内のアイコンのリソース ID を示します。 DIRID 13 の詳細については、「 [UNIVERSAL INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)」を参照してください。

スタンドアロンの .ico ファイルを参照するには、次のようなエントリを使用します。


```inf
[<DDInstall>]
AddProperty = DeviceIconProperty

[DeviceIconProperty]
DeviceIcon,,,,"%13%\vendor.ico"
```

## <a name="adding-icons-for-storage-volumes-in-explorer"></a>エクスプローラーでのストレージボリュームのアイコンの追加

シェルでは、**アイコン**および**nomediaicons**レジストリ値を使用して、デバイスを [自動再生]、[マイコンピューター]、[ファイルを開く] の各ダイアログボックスで表現します。

これらを追加するには、デバイスの[**Inf DDInstall. HW セクション**](inf-ddinstall-hw-section.md)の下に[**inf AddReg ディレクティブ**](inf-addreg-directive.md)を含めます。 次の例に示すように、[ **AddReg** ] セクションで、**アイコン**と**nomediaicons**の値のエントリを指定します。

```inf
[DDInstall.NT.HW]
AddReg = IconInformation

[IconInformation]
HKR, , Icons, 0x10000, "media-inserted-icon-file"
HKR, , NoMediaIcons, 0x10000, "no-media-inserted-icon-file"
```

次に、アイコンファイルと、それらをシステムにコピーする対応する[**Inf CopyFiles ディレクティブ**](inf-copyfiles-directive.md)を一覧表示する[**Inf SourceDisksFiles セクション**](inf-sourcedisksfiles-section.md)をインクルードします。

**アイコン**と**nomediaicons**の値のエントリは、デバイスの*ハードウェアキー*の下にある**デバイスパラメーター**キーの下に格納されます。 たとえば、に`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\<Hardware ID>\Device Parameters`は次のようなエントリが含まれます。

* `Icons [REG_MULTI_SZ] = %SystemRoot%\system32\icon.ico`

* `NoMediaIcons [REG_MULTI_SZ] = %SystemRoot%\system32\noicon.ico`

**デバイスパラメーター**キーをユーザーモードから変更するには、 [**Setupdicreatedevregkey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)または[**setupdiopendevregkey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)を使用します。

カーネルモードの場合は、 [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)を使用します。

## <a name="resources"></a>リソース

アイコンを作成するときは、[アイコン](https://docs.microsoft.com/windows/win32/uxguide/vis-icons)に示されているガイドラインに従ってください。 これらのガイドラインでは、Windows のグラフィカル要素の外観と動作を持つアイコンを作成する方法について説明します。
