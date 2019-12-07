---
title: ドライバーのインストールを簡略化する関数
description: ドライバーのインストールを簡略化する関数
ms.assetid: 7201b260-6239-4c76-8d48-7e2df9c662cd
keywords:
- 関数 WDK、ドライバーのインストールの簡略化
- DiInstallDevice
- DiInstallDriver
- DiRollbackDriver
- UpdateDriverForPlugAndPlayDevices
- PnP WDK デバイスのインストール
- WDK デバイスのインストールのプラグアンドプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c171b1adc508bde47dc8db76877e22b5c3aaeac
ms.sourcegitcommit: a97a623d64ddf573c760664be17778606e156cf5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74908297"
---
# <a name="functions-that-simplify-driver-installation"></a>ドライバーのインストールを簡略化する関数


インストールアプリケーションでは、次の機能を使用して、PnP 関数ドライバーのインストールを簡略化できます。

### <a href="" id="diinstalldevice--windows-vista-and-later-versions-of-windows-"></a>DiInstallDevice (Windows Vista 以降のバージョンの Windows)

[**Diinstalldevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)関数は、システムに存在する特定のデバイスの[ドライバーストア](driver-store.md)にプレインストールされている特定のドライバーをインストールします。

インストールアプリケーションでは、次の両方が当てはまる場合にのみ、この関数を使用する必要があります。

-   このアプリケーションには、同じ種類のデバイスインスタンスが複数組み込まれています。つまり、すべてのデバイスインスタンスが同じハードウェア Id と互換性 Id を持っています。

-   アプリケーションでは、デバイスインスタンスに固有のドライバーをインストールする必要があります。

それ以外の場合は、インストールアプリケーションで[**Diinstalldriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)または[**UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)を使用して、デバイスに最適なドライバーをインストールする必要があります。

呼び出し元は**Diinstalldevice**を呼び出して、次の操作を行うこともできます。

-   デバイスに最適なドライバーがプレインストールされていることを検索し、見つからない場合は、そのデバイスの新しいハードウェアの検出ウィザードを表示します。

-   [完了] を非表示にします。インストールページと完了-インストールアクション。

-   特定のデバイスに null ドライバーをインストールします。

-   インストールを完了するためにシステムの再起動が必要かどうかを呼び出し元に通知します。

### <a href="" id="diinstalldriver--windows-vista-and-later-versions-of-windows-"></a>DiInstallDriver (Windows Vista 以降のバージョンの Windows)

[**Diinstalldriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)関数は、ドライバー[ストア](driver-store.md)にドライバー[パッケージ](driver-packages.md)をプレインストールした後、ドライバーパッケージと一致するハードウェア ID または互換性のある id を持つ、システムに存在するすべてのデバイスにドライバーをインストールします。

**Diinstalldriver**または[**UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)を呼び出すことは、インストールアプリケーションがデバイス用の新しいドライバーをインストールする最も簡単な方法です。 **Diinstalldriver**と**UpdateDriverForPlugAndPlayDevices**は、同じ基本的なインストール操作を実行します。 ただし、 **UpdateDriverForPlugAndPlayDevices**では追加のインストールオプションがサポートされています。

既定では、デバイスに現在インストールされているドライバーよりもドライバーの方がデバイスに適合する場合にのみ、 **Diinstalldriver**はデバイスにドライバーをインストールします。 Windows がデバイスのドライバーを選択する方法の詳細については、「 [windows がドライバーを選択する方法](how-setup-selects-drivers.md)」を参照してください。

呼び出し元は**Diinstalldriver**を呼び出して、次の操作を行うこともできます。

-   ドライバーが現在デバイスにインストールされているドライバーよりもデバイスに適合するかどうかに関係なく、指定したドライバーのインストールを強制します。

    **注意**   ドライバーを強制的にインストールすると、互換性のあるドライバーまたは新しいドライバーが互換性のないドライバーまたは古いドライバーと置き換えられる可能性があります。

     

-   インストールを完了するためにシステムの再起動が必要かどうかを呼び出し元に示します。

### <a href="" id="dirollbackdriver--windows-vista-and-later-versions-of-windows-"></a>DiRollbackDriver (windows Vista 以降のバージョンの Windows)

[**DiRollbackDriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-dirollbackdriver)関数は、デバイスに対して設定されている以前にインストールされたバックアップドライバーを使用して、デバイスに現在インストールされているドライバーを置き換えます。 この機能は主に、デバイスのドライバーを更新した後にデバイスでエラーが発生した場合に、デバイスを動作状態に復元するために用意されています。 この関数は、ユーザーがデバイスマネージャーのデバイスのドライバーページで **[ドライバーのロールバック]** をクリックした場合に実行される操作と同じ操作を実行します。

Windows では、デバイスのバックアップドライバーを1つだけ保持します。 Windows は、ドライバーがデバイスに正常にインストールされた直後に、デバイスのバックアップドライバーとしてドライバーを設定し、Windows はデバイスが正しく機能していると判断します。 ただし、ドライバーがデバイスに正常にインストールされない場合、またはインストール後にデバイスが正常に機能しない場合、Windows では、デバイスのバックアップドライバーとしてドライバーが設定されません。

呼び出し元は、 **DiRollbackDriver**を呼び出して次の操作を行うこともできます。

-   ドライバーロールバックに関連付けられているユーザーインターフェイスコンポーネントの表示を抑制します。

-   インストールを完了するためにシステムの再起動が必要かどうかを呼び出し元に示します。

ドライバーのロールバックの詳細については、ヘルプとサポートセンターのデバイスマネージャーに関する情報を参照してください。

### <a href="" id="updatedriverforplugandplaydevices"></a>UpdateDriverForPlugAndPlayDevices

[**UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)関数は、ドライバーパッケージと一致するハードウェア id または互換性のある id を持つ、システムに存在するすべてのデバイスにドライバーをインストールします。

この関数または[**Diinstalldriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)を呼び出すことは、システム内のデバイスに最適な新しいドライバーをインストールするための最も簡単な方法です。 **UpdateDriverForPlugAndPlayDevices**の基本的な操作は、 **diinstalldriver**の操作に似ています。 ただし、 **UpdateDriverForPlugAndPlayDevices**では追加のインストールオプションがサポートされています。

既定では、 **UpdateDriverForPlugAndPlayDevices**は、ドライバーがデバイスに現在インストールされているドライバーよりもデバイスに一致する場合にのみ、デバイスにドライバーをインストールします。

呼び出し元は、必要に応じて**UpdateDriverForPlugAndPlayDevices**を呼び出して、次の操作を行うこともできます。

-   ドライバーが現在デバイスにインストールされているドライバーよりもデバイスに適合するかどうかに関係なく、指定したドライバーのインストールを強制します。

    **注意**   ドライバーを強制的にインストールすると、互換性のあるドライバーまたは新しいドライバーが互換性のないドライバーまたは古いドライバーと置き換えられる可能性があります。

     

-   インストールファイルのコピー、名前の変更、または削除を抑制します。

-   ユーザーインターフェイスコンポーネントの表示を抑制します。

-   インストールを完了するためにシステムの再起動が必要かどうかを呼び出し元に示します。

 

 





