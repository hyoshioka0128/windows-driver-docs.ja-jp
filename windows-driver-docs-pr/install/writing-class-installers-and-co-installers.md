---
title: クラス インストーラーと共同インストーラーの記述
description: クラス インストーラーと共同インストーラーの記述
ms.assetid: DA52A2C4-81D7-4e95-97CD-D5A1C625CE02
keywords:
- 書き込み、クラスのインストーラー WDK デバイス インストール
- クラスのインストーラー WDK デバイス インストールの作成
- 書き込む co-installer WDK のデバイス インストール
- co-installer を WDK デバイスのインストールに書き込む
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0337a4062121a78ad9f2616f4713986842d683e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363475"
---
# <a name="writing-class-installers-and-co-installers"></a>クラス インストーラーと共同インストーラーの記述


**注**  ユニバーサルまたはモバイルのドライバー パッケージでは、このセクションで説明する機能はサポートされていません。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

このセクションに記述するときに従う必要のあるガイドラインが含まれています、*共同インストーラー*:

[ユーザー インターフェイスを表示します。](#displaying-a-user-interface)

[デバイス インストール状態の保存](#saving-device-installation-state)

[実行可能ファイルまたは DLL ファイルの読み込み](#loading-executable-or-dll-files)

[他のプロセスやサービスを開始](#starting-other-processes-or-services)

共同インストーラーを作成する方法の詳細については、次を参照してください。[共同インストーラーの作成](writing-a-co-installer.md)です。

## <a name="displaying-a-user-interface"></a>ユーザー インターフェイスを表示します。


デバイスのインストールは、ほとんどの場合、システムの (非対話型) サービスで実行されます。 そのため、ユーザーは表示またはこのコンテキストで表示される任意のユーザー インターフェイスに応答できません。 提供されている任意のダイアログ ボックス*共同インストーラー*の処理中に、[デバイス インストール機能 (差分) コード](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))により、デバイスのインストールが応答を停止します。

ほとんどの場合、共同インストーラーと対話しない以外ではユーザーの処理中に、[完了-インストール アクション](finish-install-actions--windows-vista-and-later-.md)します。 完了-インストール アクションは、対話型のコンテキストで実行します。

**注**  デバイスのインストールが失敗する原因となったため、共同インストーラーは ERROR_REQUIRES_INTERACTIVE_WINDOWSTATION で差分コード失敗しません。 デバイスのインストールは、ユーザーの介入を必要とする場合、共同インストーラーは完了インストール操作をサポートします。

 

## <a name="saving-device-installation-state"></a>デバイス インストール状態の保存


内のデバイス インストール状態を保存しないで、*共同インストーラー*ダイナミック リンク ライブラリ (DLL) です。 差分コードは、インストーラーによって処理された後、Windows は一般に DLL をアンロードするため、この DLL 内に保存されているすべての状態情報は保持されません。

インストーラーのデバイスの状態を安全に保持するには、クラスのインストーラーや共同インストーラーする必要があります、状態情報を保存、デバイスの内のプロパティとして*ドライバー キー*レジストリにします。 これを行うには、次の手順に従います。

1.  ドライバーのキーを識別するレジストリのハンドルを取得する、*デバイス インスタンス*を使用して、 [ **SetupDiOpenDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)で、 *KeyType*パラメーターDIREG_DRV に設定します。

2.  使用[ **SetupDiGetDevicePropertyKeys** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys) (デバイスのインスタンスのすべてのプロパティのキーを取得) するまたは[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)(指定したデバイス インスタンス プロパティのキーを取得する) にします。

3.  使用[ **SetupDiSetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)デバイス インスタンスのプロパティのキーを保存します。

## <a name="loading-executable-or-dll-files"></a>実行可能ファイルまたは DLL ファイルの読み込み


場合、*共同インストーラー* Windows 64 ビット プラットフォーム、オペレーティング システムで、署名されていない実行可能ファイルまたは DLL を読み込むようにしようからこのセキュリティで保護された環境に読み込まれるようにします。

安全に、クラスのインストーラー ファイルまたは共同インストーラーによって、実行可能ファイルまたは DLL を読み込み、強くお勧め、実行可能ファイルまたは DLL が含まれることで、デジタル署名された[ドライバー パッケージ](driver-packages.md)します。 ドライバー パッケージに署名する方法の詳細については、次を参照してください。[ドライバーの署名](driver-signing.md)します。

**注**  クラスのインストーラーと共同インストーラー読み込む必要がありますいない DLL モジュール明示的な関数の呼び出しによってなど**LoadLibrary**、または依存関係のリンクを作成しています。

 

## <a name="starting-other-processes-or-services"></a>他のプロセスやサービスを開始


デバイスのインストール中には、Windows は追加のプロセスを追跡することはできず、行っているかは終了ときを判断できません。 たとえば、Windows でしたまたは開始または停止、デバイス、プロセスの重要な動作が実行中にシステムの再起動を開始します。

ほとんどの場合、 *co-installer*他のプロセスまたはサービスを開始する必要があります。 、インストーラーを開始できます他のプロセスに安全に呼び出すことによって[CreateProcess](https://go.microsoft.com/fwlink/p/?linkid=194524)関数またはを通じて表示されるダイアログから、[完了-インストール アクション](finish-install-actions--windows-vista-and-later-.md)します。 インストーラーは、作成されたプロセスが終了するまで、ダイアログまたはプロシージャに引き続きユーザーをできないする必要があります。

 

 





