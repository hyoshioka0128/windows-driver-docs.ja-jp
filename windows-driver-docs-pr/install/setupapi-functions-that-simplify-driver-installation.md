---
title: ドライバーのインストールを簡略化する SetupAPI 関数
description: ドライバーのインストールを簡略化する SetupAPI 関数
ms.assetid: 7201b260-6239-4c76-8d48-7e2df9c662cd
keywords:
- SetupAPI 関数 WDK、ドライバーのインストールを簡略化します。
- DiInstallDevice
- DiInstallDriver
- DiRollbackDriver
- UpdateDriverForPlugAndPlayDevices
- PnP WDK デバイスのインストール、SetupAPI
- プラグ アンド プレイ WDK デバイス インストールでは、SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14f781b80d64c58948d0f8fe602968dec8cfd256
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348660"
---
# <a name="setupapi-functions-that-simplify-driver-installation"></a>ドライバーのインストールを簡略化する SetupAPI 関数


インストール アプリケーションでは、関数の PnP ドライバーのインストールを簡略化するのに次の SetupAPI 関数を使用できます。

### <a href="" id="diinstalldevice--windows-vista-and-later-versions-of-windows-"></a> DiInstallDevice (Windows Vista および Windows の以降のバージョン)

[ **DiInstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff544710)関数では、プレインストールされている特定のドライバーのインストール、[ドライバー ストア](driver-store.md)システムに存在する特定のデバイス。

インストール アプリケーションでは、次の両方に該当する場合は、この関数を使用するのみ。

-   アプリケーションには、同じ型の 1 つ以上のデバイス インスタンスが組み込まれています、同じハードウェア Id および互換性 Id、つまり、デバイスのすべてのインスタンスがあります。

-   アプリケーションでは、デバイス固有のインスタンスのドライバーがデバイスのインスタンスにインストールすることが必要です。

それ以外の場合、インストール アプリケーションで使用する[ **DiInstallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff544717)または[ **UpdateDriverForPlugAndPlayDevices** ](https://msdn.microsoft.com/library/windows/hardware/ff553534)をインストールするにはデバイスに最適なものであるドライバー。

呼び出し元が呼び出すことができますも**DiInstallDevice**以下を実行します。

-   プレインストールされているドライバー、デバイスに最適な一致を検索し、いずれかが存在しない場合は、デバイスの新しいハードウェアの検出ウィザードを表示します。

-   -インストールが [完了] ページの呼び出しを抑制して、アクションのインストールが完了します。

-   特定のデバイスには、null のドライバをインストールします。

-   インストールを完了するシステムの再起動が必要かどうかを呼び出し元に通知します。

### <a href="" id="diinstalldriver--windows-vista-and-later-versions-of-windows-"></a> DiInstallDriver (Windows Vista および Windows の以降のバージョン)

[ **DiInstallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff544717)関数のプレインストール、[ドライバー パッケージ](driver-packages.md)で、[ドライバー ストア](driver-store.md)し、すべてのデバイスで、ドライバーをインストールしますID またはドライバー パッケージと一致する互換性 ID は、ハードウェアのあるシステムに存在します。

呼び出す**DiInstallDriver**または[ **UpdateDriverForPlugAndPlayDevices** ](https://msdn.microsoft.com/library/windows/hardware/ff553534)デバイス用の新しいドライバーをインストールするインストール アプリケーションの最も簡単な方法です。 **DiInstallDriver**と**UpdateDriverForPlugAndPlayDevices**同じ基本的なインストール操作を実行します。 ただし**UpdateDriverForPlugAndPlayDevices**追加のインストール オプションをサポートしています。

既定では、 **DiInstallDriver**ドライバーがデバイスに現在インストールされているドライバーよりもデバイスに最適である場合のみをデバイスに、ドライバーをインストールします。 Windows デバイスのドライバーを選択する方法については、次を参照してください。 [Windows ドライバーを選択する方法](how-setup-selects-drivers.md)します。

呼び出し元が呼び出すことができますも**DiInstallDriver**以下を実行します。

-   ドライバーは、デバイスに現在インストールされているドライバーよりも、デバイスに合わせて、かどうかに関係なく、指定したドライバーのインストールを強制します。

    **注意**  ドライバーのインストールが強制されることがあまりに互換性があるか、古いドライバーより互換性があるか、新しいドライバーを置き換えます。

     

-   呼び出し元に、インストールを完了するシステムの再起動が必要かどうかを示します。

### <a href="" id="dirollbackdriver--windows-vista-and-later-versions-of-windows-"></a> DiRollbackDriver (Windows Vista および Windows の以降のバージョン)

[ **DiRollbackDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff544721)関数は現在のデバイスをデバイスに設定されているバックアップ ドライバーのインストールにインストールされているドライバーを置き換えます。 この関数は、デバイスのドライバーを更新した後、デバイスが失敗した場合、デバイスを稼働状態に復元するには、主に提供されます。 この関数は、ユーザーがクリックされた場合に実行される同じ操作を実行**ドライバーのロールバック**デバイス マネージャーでデバイス ドライバーのページ。

Windows では、最大でデバイスの 1 つのバックアップ ドライバーを保持します。 Windows では、バックアップ デバイスのドライバーをドライバーが正常にデバイスと Windows のインストール後すぐには、デバイスが正しく機能していることを判断すると、ドライバーを設定します。 ただし、デバイス ドライバーが正常にインストールされませんまたはインストール後、デバイスが正しく機能しない、Windows は設定されません、ドライバー、デバイスのバックアップ ドライバーとして。

呼び出し元が呼び出すことができますも**DiRollbackDriver**以下を実行します。

-   ドライバーのロールバックに関連付けられているすべてのユーザー インターフェイス コンポーネントを表示しないようにします。

-   呼び出し元に、インストールを完了するシステムの再起動が必要かどうかを示します。

ドライバーのロールバックの詳細については、デバイス マネージャーのヘルプとサポート センターでについてを参照してください。

### <a href="" id="updatedriverforplugandplaydevices"></a> UpdateDriverForPlugAndPlayDevices

[ **UpdateDriverForPlugAndPlayDevices** ](https://msdn.microsoft.com/library/windows/hardware/ff553534)関数は、すべてのデバイスで、システムに存在するハードウェア ID またはドライバー パッケージと一致する互換性のある ID を持つドライバーをインストールします。

この関数の呼び出しまたは[ **DiInstallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff544717)インストール アプリケーション、システム内のデバイスに最適なものである新しいドライバーをインストールする最も簡単な方法です。 基本的な操作**UpdateDriverForPlugAndPlayDevices**の操作に似ています**DiInstallDriver**します。 ただし**UpdateDriverForPlugAndPlayDevices**追加のインストール オプションをサポートしています。

既定では、 **UpdateDriverForPlugAndPlayDevices**ドライバーがデバイスに現在インストールされているドライバーよりもデバイスに最適である場合のみをデバイスに、ドライバーをインストールします。

呼び出し元が呼び出すことができますも**UpdateDriverForPlugAndPlayDevices**以下を実行します。

-   ドライバーは、デバイスに現在インストールされているドライバーよりも、デバイスに合わせて、かどうかに関係なく、指定したドライバーのインストールを強制します。

    **注意**  ドライバーのインストールが強制されることがあまりに互換性があるか、古いドライバーより互換性があるか、新しいドライバーを置き換えます。

     

-   コピー、名前の変更、またはインストール ファイルの削除を抑制します。

-   ユーザー インターフェイス コンポーネントを表示しないようにします。

-   呼び出し元に、インストールを完了するシステムの再起動が必要かどうかを示します。

 

 





