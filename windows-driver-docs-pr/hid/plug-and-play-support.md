---
title: プラグ アンド プレイのサポート
description: このセクションでは、ユニバーサル シリアル バスで列挙プロセスについて説明します。
ms.assetid: CB3D76DB-4A96-4A19-BC1C-C9181A12B04E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43b79780964ab0a94bd066cad6d243d55a62e6d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572188"
---
# <a name="plug-and-play-support"></a>プラグ アンド プレイのサポート


このセクションでは、ユニバーサル シリアル バスで列挙プロセスについて説明します。

デバイスが Windows ベースのコンピューターに接続されて、Windows USB スタック、デバイスのインターフェイスの記述子 (または記述子) を含め、デバイスからの詳細を抽出して、デバイスを列挙およびハードウェア Id および互換性 Id のセットが生成されます。デバイスです。

USB ハードウェア Id の完全な一覧は、デバイスのインストール 「デバイスの識別文字列」セクションを参照してください。

次のセクションでは、次の例は、2 つのシナリオを示しています。

-   1 つのインターフェイスの USB デバイスの USB Id
-   複数のインターフェイス (複合) USB デバイスの USB Id

*例 1:1 つのインターフェイスの HID USB デバイス*

この例では、Windows 2000 または Windows XP を実行するシステム上の単一インターフェイス USB デバイスのハードウェア Id および互換性 Id の生成方法を示します。

USBHUB ドライバーが抽出 USB スタックによって、デバイスが列挙される最初と**idVendor**、 **idProduct**、および**bcdDevice**デバイス記述子から。 USB ハードウェア ID を生成するこれら 3 つのフィールドが組み込まれています 仕入先、デバイス、およびリビジョン番号は常に 16 進形式で格納することに注意してください。

デバイスの互換性のある ID の生成より複雑です。 クラスのコード、サブクラス コード、およびプロトコルのコードはインターフェイス記述子ので決まります**bInterfaceClass**、 **bInterfaceSubClass**、および**bInterfaceProtocol**します。 これらの値は、2 桁の 16 進形式では。

**注**  、INF を提供する場合、ハードウェア id が一致する必要があります、**太字**次の表の左の列の識別子。 (使用しないように、右側の列に表示されている互換性のある識別子。)

 

|                                        |                                      |
|----------------------------------------|--------------------------------------|
| ハードウェア Id                   | 互換性のある識別子               |
| **USB\\Vid\_xxxx & Pid\_yyyy & Rev\_zzzz** | USB\\クラス\_aa & サブクラス\_ポート (&)、bb\_cc |
| **USB\\Vid\_xxxx & Pid\_yyyy**           | USB\\クラス\_aa & サブクラス\_bb          |
|                                        | USB\\クラス\_aa                       |

 

*例 2:複数のインターフェイス/関数 HID USB デバイス (複合デバイス)*

USB デバイスは複数の関数は、複合デバイスと呼ばれます。 この例では、Windows での複合 USB デバイスのハードウェア Id および互換性 Id の生成方法を示します。 新しい USB 複合デバイスが Windows を実行するコンピューター システムに接続されている USBHUB ドライバーは物理デバイス オブジェクト (PDO) を作成し、オペレーティング システム、デバイスの子のセットが変更されたことを通知します。 ハードウェア Id に関連付けられた新しい PDO のハブのドライバーのクエリを実行するには後、は、システムは、識別子と一致するものを該当する INF ファイルを検索します。 仕入先が、オペレーティング システムが取得するを防ぐためにハードウェア ID の一致を指定する必要があります仕入先がデバイス全体 (つまり、複合デバイス ドライバーを使用していない、) の 1 つのドライバーを読み込むし、そのドライバーを使用したソフトウェアのすべてのインターフェイスを多重化することを選択する場合、下のランク付けの一致 (USB\\複合)。

**注**  、INF を提供する場合、ハードウェア id が一致する必要があります、**太字**次の表の左の列の識別子。 (使用しないように、右側の列に表示されている互換性のある識別子。)

 

|                                        |                                      |
|----------------------------------------|--------------------------------------|
| ハードウェア Id                   | 互換性のある識別子               |
| **USB\\Vid\_xxxx & Pid\_yyyy & Rev\_zzzz** | USB\\クラス\_aa & サブクラス\_ポート (&)、bb\_cc |
| **USB\\Vid\_xxxx & Pid\_yyyy**           | USB\\クラス\_aa & サブクラス\_bb          |
|                                        | USB\\クラス\_aa                       |
|                                        | USB\\複合                       |

 

プラグ アンド プレイの Windows では、USB を使用して、ただし、ハードウェアの一致が見つからない場合は、\\複合識別子 (USBCCGP) 汎用的な親の USB ドライバーをロードします。 次に、一般的な親ドライバーは別のインターフェイスごとに複合デバイス、ハードウェア Id のセットで Pdo (すべてのインターフェイスの 1 つ) の個別セットを作成します。 次のセクションでは、子 Pdo のハードウェア Id の形式が表示されます。

USBCCGP ドライバー各インターフェイスの PDO のハードウェア Id のセットをビルドするには、ハードウェア ID の末尾に (つまり、0 から始まる 16 進値) インターフェイスの数を追加します

クラスのコード、サブクラス コード、およびプロトコルのコードによって決まりますが、 **bInterfaceClass**、 **bInterfaceSubClass**、および**bInterfaceProtocol**インターフェイスのフィールド記述子では、それぞれします。 これらの値は、2 桁の 16 進形式では。

**注**  ドライバーをロードするか、デバイスのフレンドリ名を指定する、ハードウェア id が一致する INF を提供する場合、**太字**次の表の左の列の識別子。 (使用しないように、右側の列に表示されている互換性のある識別子。)

 

|                                               |                                      |
|-----------------------------------------------|--------------------------------------|
| ハードウェア Id                          | 互換性のある識別子               |
| **USB\\Vid\_xxxx&Pid\_yyyy&Rev\_zzzz&MI\_ww** | USB\\クラス\_aa & サブクラス\_ポート (&)、bb\_cc |
| **USB\\Vid\_xxxx&Pid\_yyyy&MI\_ww**           | USB\\クラス\_aa & サブクラス\_bb          |
|                                               | USB\\クラス\_aa                       |

 

 

 



