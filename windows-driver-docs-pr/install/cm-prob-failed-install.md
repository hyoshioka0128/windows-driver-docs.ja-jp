---
title: CM_PROB_FAILED_INSTALL
description: CM_PROB_FAILED_INSTALL
ms.assetid: d65f1f14-e455-4902-8168-38d8ae51f81f
keywords:
- CM_PROB_FAILED_INSTALL
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 59561c6446119615dc2b0e59cf00958922ef3722
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279571"
---
# <a name="code-28---cm_prob_failed_install"></a>コード 28-CM_PROB_FAILED_INSTALL

このデバイスマネージャーエラーメッセージは、デバイスのドライバーがインストールされていないことを示します。

## <a name="error-code"></a>エラー コード

28

### <a name="display-message"></a>メッセージの表示

"このデバイスのドライバーはインストールされていません。 (コード 28) "

### <a name="recommended-resolution"></a>推奨される解決策

デバイスを製造している会社の web サイトにアクセスし、このデバイスの最新のドライバーを探してください。


## <a name="for-driver-developers"></a>ドライバー開発者向け

デバイスの[**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)プロパティは、エラーコードを示している必要があります。

### <a name="0xc0000490---status_pnp_no_compat_drivers"></a>0xC0000490-STATUS_PNP_NO_COMPAT_DRIVERS

PnP は、デバイスと互換性のあるドライバーを見つけることができませんでした。 このエラーは、"DNF (ドライバーが見つかりません)" 問題と呼ばれることがよくあります。

問題となっているデバイスのハードウェア Id と互換性のある Id を調べ、[[**モデル] セクション**](inf-models-section.md)で INF によって指定されたハードウェア id と比較します。  また、[モデル] セクションの名前の**TargetOSVersion**部分が、実行しているアーキテクチャと OS のバージョンに適用されていることを確認します。

### <a name="0xc0000491---status_pnp_driver_package_not_found"></a>0xC0000491-STATUS_PNP_DRIVER_PACKAGE_NOT_FOUND

このコードは、ドライバーパッケージの依存関係がないことを示します。

具体的には、デバイスで一致した INF は、[ [Inf DDInstall] セクション](inf-ddinstall-section.md)の [エントリを**含める**] を使用して、このバージョンの Windows には存在しない Microsoft 提供の inf を指定します。

### <a name="0xc0000492---status_pnp_driver_configuration_not_found"></a>0xC0000492-STATUS_PNP_DRIVER_CONFIGURATION_NOT_FOUND

このコードは、ドライバーパッケージの依存関係がないことも示しています。

この場合、デバイスで一致する INF は、[ [Inf DDInstall] セクション](inf-ddinstall-section.md)**のエントリを**使用して、 **Include**ディレクティブで参照されている Microsoft 提供の INF に存在しないセクションを指定します。

### <a name="0xc0000494---status_pnp_function_driver_required"></a>0xC0000494-STATUS_PNP_FUNCTION_DRIVER_REQUIRED

このエラーは、INF で、関連付けられた関数ドライバーサービスが指定されていない場合に発生します。

次のいずれかを確認します。

1. インストールするデバイスの INF ファイルには、 [**addservice ディレクティブ**](inf-addservice-directive.md)が含まれています。このディレクティブを使用して、関連付けられたサービスまたは関数ドライバーをフラグ SPSVCINST_ASSOCSERVICE (0x00000002) を使用して設定します。
2. INF ファイルでは、システム提供のドライバーを参照する[Inf DDInstall セクション](inf-ddinstall-section.md)の**Include**または**必要**なエントリを指定します。これにより、デバイスに関連付けられたサービスが設定されます。

### <a name="upgrade-to-windows-10"></a>Windows 10 へのアップグレード

アップグレードする前に、デバイスにドライバーがあり、正常に動作しています。 アップグレード後にコード28が表示されます。 この問題は、多くの場合、ドライバーパッケージが移行から除外されていることが原因で発生します。
