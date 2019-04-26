---
title: カスタマイズされたプリンター セットアップの操作
description: カスタマイズされたプリンター セットアップの操作
ms.assetid: 888125e9-a057-4e86-9df8-0086cedb368d
keywords:
- カスタマイズされたプリンター セットアップ操作 WDK
- WDK の INF ファイルを印刷するカスタマイズされたセットアップの操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc66fda7ef33a0a7acde11cddce024cb5383944a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355686"
---
# <a name="customized-printer-setup-operations"></a>カスタマイズされたプリンター セットアップの操作





含める Ntprint.dll、既定の Windows 2000、およびプリンター クラスの以降のインストーラーを使用してインストールされているプリンターのカスタマイズされたプリンター セットアップの操作を提供することができます、 **VendorSetup**プリンターの INF ファイルの INF エントリ。

**重要な**  :注意してくださいを**VendorSetup**現在は非推奨し、で使用する必要がありますいない*新しい*v3 または v4 ドライバーを開発します。 このトピックでは、既にこの INF ディレクティブを使用している既存の v3 ドライバーのメンテナンスのみ、または参照に対して提供されます。

 

**注**  プリンター ドライバーのインストール中にユーザー インターフェイス要素を表示する場合は、使用する必要あります、 **VendorSetup** INF エントリ。 ただし、使用する必要があります、 **VendorSetup** INF エントリがどうしても必要な場合にのみです。 重大な欠点は、その使用からプラグ アンド プレイが (ユーザーは、管理者をここである必要があります) を使用してプリンターをインストールする通常のユーザーによって禁止されています。
デバイス ドライバーが署名するとき、または (符号付きまたは符号なし) ドライバーの INF ファイルが含まれている場合、サーバー側のインストールを使用してデバイスをインストールすることはできません、 **VendorSetup** INF エントリ。 ドライバーが署名されていないときに、セットアップは署名されたドライバーの場合は、ドライバーのランクに 0x8000 を追加します。 ドライバーの INF ファイルが含まれている場合、 **VendorSetup**エントリ、セットアップは、デバイスのインストールは (サーバー側のインストールで発生することはできません) をユーザーの介入を必要とし、インストールを停止を決定します。 セットアップは、ドライバーのランクは 0x8000 場合もサーバー側のインストールを停止または拡大します。 クライアント側のインストールとデバイスのインストールが再起動する時に、管理者特権を持つユーザーがログインしたときに、インストールを続行できます。 ランクが 0x1000 ドライバーのまたは大きくなるとは、そのため、ハードウェア ID が一致のセットアップが新しいデバイスの DLL は、ドライバーをインストールするユーザーを要求で新しいハードウェアの検出ウィザードが起動されます。 署名されたドライバーの INF ファイルが含まれている場合、 **VendorSetup**エントリ、およびドライバーのランクは 0x1000 より小さい、セットアップが新しいハードウェアの検出ウィザードを起動できません。 詳細については、次を参照してください。[デバイス インストール コンポーネント](https://msdn.microsoft.com/library/windows/hardware/ff541277)と[セットアップによるドライバーの選択](https://msdn.microsoft.com/library/windows/hardware/ff546228)します。

 

形式、 **VendorSetup**エントリを次に示します。

VendorSetup = *FileName*、 *FunctionName*

場所*FileName*セットアップ関数では、含んでいる DLL の名前を指定および*FunctionName*関数の名前を指定します。 %Windir% で DLL をインストールする必要があります\\system32 ディレクトリ。 プリンター クラスのインストーラーは、プラグ アンド プレイまたはプリンターの追加ウィザード、プリンターがインストールされている場合にのみ、この DLL のセットアップ関数を呼び出します。 (たとえば、プリンター ドライバーの追加ウィザードの使用) でのみ、ドライバーがインストールされている場合は、セットアップ関数は呼び出されません。

1 つまたは複数のファイルを %windir% にコピーする\\system32 ディレクトリ、INF ライター定義のセクションの名前を追加するには、INF を**DestinationDirs**セクション。 OEMVendorFiles セクションには、次の例では、ファイルのコピーをすべて一覧表示します。

```cpp
[DestinationDirs]
OEMVendorFiles = 11
...
[OEMVendorFiles]
vendor.dll
```

指定された関数*FunctionName*次のプロトタイプに一致する必要があります。

`VOID WINAPI         `*FunctionName*`(HWND         hWnd, HINSTANCE hInstance, LPSTR lpszCmdLine, UINT  nCmdShow);`

場所*FunctionName*セットアップ関数の名前を指定します。 関数のパラメーターとその説明は、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>hWnd</em></p></td>
<td><p>親ウィンドウのハンドルを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>hInstance</em></p></td>
<td><p>呼び出し元のプロセスのインスタンス ハンドルを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>lpszCmdLine</em></p></td>
<td><p>インストールしたプリンターの名前を含む、ANSI 文字列を指定します。 この文字列は解析<em>FunctionName</em>します。</p></td>
</tr>
<tr class="even">
<td><p><em>nCmdShow</em></p></td>
<td><p>ウィンドウの表示方法を指定します。 ウィンドウを表示する方法を制御するフラグは、Winuser.h で定義されます。</p></td>
</tr>
</tbody>
</table>

 

プリンター クラスのインストーラーは、インストール操作の最後の手順の 1 つとして、セットアップ関数を呼び出します。

 

 




