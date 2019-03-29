---
title: Windows との統合
description: Windows との統合
ms.assetid: 57721e38-5974-4080-b051-93b78a7f42c6
keywords:
- プロパティ シートの WDK DirectInput、登録します。
- ゲーム コント ローラー WDK DirectInput、登録
- コントロール パネルの WDK DirectInput、登録
- プロパティ シートの WDK DirectInput、Windows の統合
- ゲーム コント ローラー WDK DirectInput、Windows の統合
- コントロール パネルの WDK DirectInput、Windows の統合
- Windows 統合 WDK DirectInput コントロール パネル
- プロパティ シートを登録します。
- DirectInput コントロール パネルのデバイスの登録
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f3649c75c807479fc1040577ded80728582ce405
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463900"
---
# <a name="integration-with-windows"></a>Windows との統合





プロパティ シートのページは、COM オブジェクトであるため、登録する必要があります。 これ行う、INF ファイル、または DirectInput の**IDirectInputJoyConfig8**インターフェイス。 サンプルの INF ファイルとは、サンプルのプロパティ シート DirectX ドライバー開発キット (DDK) の一部です。

**プロパティ シートのページを登録するには。**

1.  プロパティ シートの CLSID を作成する (これは、Microsoft Windows SDK に含まれています) GuidGen ツールを使用して (これに入力したものと同じ、 **ConfigCLSID**エントリが前に説明した)。 ただし、これは、デバイス固有のプロパティ シート GUID と、コード内と同じである必要があります。

2.  下のレジストリに新しいキーを作成**マイ コンピューター\\HKEY\_クラス\_ルート\\CLSID** (そのようになります {この新しい GUID を使用してB9EA2BE1-E8E9-11D0-9880-00AA0044480F})。

3.  という名前のサブキーを作成、そのキー内で**InProcHandler32**と**InProcServer32**します。

4.  内で、 **InProcServer32**キー、プロパティ シート DLL の名前と場所を反映するように (既定値) のエントリを編集します。

ゲーム デバイスとして、デバイスが正しく登録されてもする必要があります。 これは、DirectInput、または、INF ファイルを通じて行うことがあります。

**デバイスを登録します。**

1.  レジストリ キーに**マイ コンピューター\\HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\MediaProperties\\PrivateProperties\\ジョイスティック\\OEM**デバイスのキーを入力します。 このキーを作成することをお勧めデバイス OEM の名前と同じ名前を付けます。

2.  次のエントリを作成します。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>キーの値</th>
    <th>キー値の型</th>
    <th>キーの値の型の内容</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ConfigCLSID</p></td>
    <td><p>文字列値</p></td>
    <td><p>「{プロパティ シート CLSID}」</p></td>
    </tr>
    <tr class="even">
    <td><p>OEMName</p></td>
    <td><p>文字列値</p></td>
    <td><p>「デバイスの製品名」</p></td>
    </tr>
    </tbody>
    </table>

     

**注**  これら 2 つのエントリは、最小値を開始する必要があります。 詳細については、すべての利用可能なエントリとその関連サービスは、DirectX DDK を参照してください。

 

 

 




