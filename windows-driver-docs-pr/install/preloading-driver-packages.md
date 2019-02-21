---
title: ドライバー パッケージの事前読み込み
description: ドライバー パッケージの事前読み込み
ms.assetid: e617764d-0b48-4cd8-aeac-04d6039aba71
keywords:
- インストール アプリケーション WDK、事前に読み込まれたドライバー パッケージ
- デバイスのインストール アプリケーション WDK、事前に読み込まれたドライバー パッケージ
- 事前に読み込まれたドライバー パッケージ WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70c02af27baab235d5f4d857d4be127a855b8371
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531081"
---
# <a name="preloading-driver-packages"></a>ドライバー パッケージの事前読み込み


プラグ アンド プレイ (PnP)[ドライバー パッケージ](driver-packages.md)できる*プリロード*またはコンピューターで Windows をインストールした後、Windows インストールの一部としてコンピューターにします。 ネットワーク管理者は、ネットワーク コンピューターにインストールされているドライバー パッケージのソースを提供するネットワーク サーバー上のドライバー パッケージをプリロードすることもします。 Windows は、デバイスと一致するドライバーを検索する場合、Windows は、デバイスに一致する事前に読み込まれたドライバー パッケージがあるかどうかを確認します。

ドライバー パッケージを事前に Windows インストールを構成する方法は、このドキュメントの範囲外です。 ドライバー パッケージを事前に Windows インストールを構成する方法については、次を参照してください[追加 OEM プラグ アンド プレイ ドライバーを Windows XP 方法](https://go.microsoft.com/fwlink/p/?linkid=3100&ID=314479)と[追加 OEM プラグ アンド プレイ ドライバーを Windows インストール方法](https://go.microsoft.com/fwlink/p/?linkid=70235).

Windows をインストールした後、[ドライバー パッケージ](driver-packages.md)で、次の方法のいずれかの事前読み込みを行うことができます。

1.  ローカル コンピューター上のドライバー パッケージを事前にドライバー パッケージをローカル コンピューター上の特定のパッケージ ディレクトリにコピーしするドライバー パッケージのローカル ディレクトリ パスの連結、 **DevicePath** の下のエントリの値**HKLM\\ソフトウェア\\Microsoft\\Windows\\CurrentVersion**レジストリのサブキー。

2.  コンピューターのネットワークのドライバー パッケージを事前にネットワーク管理者は、ドライバー パッケージをネットワーク サーバー上の共有ディレクトリにコピーし、共有ディレクトリのパスを連結、 **DevicePath**内のエントリの値、共有ディレクトリへのアクセス権を持つネットワーク コンピューターのレジストリ。

**DevicePath**値のエントリは、 [REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-エントリを含む型指定された、 *%systemroot%\\inf*ディレクトリのパスと 0 個以上のディレクトリ パスエントリ。 形式、 **DevicePath**値のエントリは、次は、各ディレクトリ パスは、ローカル ディレクトリ パスまたはネットワーク サーバー上の共有ディレクトリのパスを事前に読み込まれた[ドライバー パッケージ](driver-packages.md)が配置されています。

```cpp
%SystemRoot%\inf;DirectoryPath1;DirectoryPath2;...
```

ネットワーク アダプターのドライバー パッケージの事前読み込みなど、 *%systemroot%\\ドライバー\\NIC*管理者であるローカル コンピューター上のディレクトリは、そのディレクトリにドライバー パッケージをコピーし、パスの連結、 **DevicePath**エントリの値を次のようにします。

```cpp
%SystemRoot%\inf;...;%SystemRoot%\inf\Drivers\NIC
```

たとえば、共有ディレクトリ内のネットワーク アダプターのドライバー パッケージを事前に読み込む *\\ \\DriverPackageServer\\ShareName\\ドライバー\\NIC*ネットワークでは、ネットワーク管理者は、共有ディレクトリにドライバー パッケージをコピーしの共有ディレクトリのパスを連結、 **DevicePath**次のように、ネットワーク コンピューターのレジストリのエントリの値します。

```cpp
%SystemRoot%\inf;...;\\DriverPackageServer\ShareName\Drivers\NIC
```

 

 





