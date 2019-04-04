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
ms.openlocfilehash: 2be547e9a6744009398545ce3e6191ee1a068e81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573028"
---
# <a name="writing-class-installers-and-co-installers"></a>クラス インストーラーと共同インストーラーの記述


**注**  ユニバーサルまたはモバイルのドライバー パッケージでは、このセクションで説明する機能はサポートされていません。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

このセクションに記述するときに従う必要のあるガイドラインが含まれています、*共同インストーラー*:

[ユーザー インターフェイスを表示します。](#displaying-a-user-interface)

[デバイス インストール状態の保存](#saving-device-installation-state)

[実行可能ファイルまたは DLL ファイルの読み込み](#loading-executable-or-dll-files)

[他のプロセスやサービスを開始](#starting-other-processes-or-services)

共同インストーラーを作成する方法の詳細については、[共同インストーラーの作成](writing-a-co-installer.md)を参照してください。

## <a name="displaying-a-user-interface"></a>ユーザー インターフェイスを表示します。


デバイスのインストールは、ほとんどの場合、システムの (非対話型) サービスで実行されます。 そのため、ユーザーは表示またはこのコンテキストで表示される任意のユーザー インターフェイスに応答できません。 提供されている任意のダイアログ ボックス*共同インストーラー*の処理中に、[デバイス インストール機能 (差分) コード](https://msdn.microsoft.com/library/windows/hardware/ff541307)により、デバイスのインストールが応答を停止します。

ほとんどの場合、共同インストーラーと対話しない以外ではユーザーの処理中に、[完了-インストール アクション](finish-install-actions--windows-vista-and-later-.md)します。 完了-インストール アクションは、対話型のコンテキストで実行します。

**注**  デバイスのインストールが失敗する原因となったため、共同インストーラーは ERROR_REQUIRES_INTERACTIVE_WINDOWSTATION で差分コード失敗しません。 デバイスのインストールは、ユーザーの介入を必要とする場合、共同インストーラーは完了インストール操作をサポートします。

 

## <a name="saving-device-installation-state"></a>デバイス インストール状態の保存


内のデバイス インストール状態を保存しないで、*共同インストーラー*ダイナミック リンク ライブラリ (DLL) です。 差分コードは、インストーラーによって処理された後、Windows は一般に DLL をアンロードするため、この DLL 内に保存されているすべての状態情報は保持されません。

インストーラーのデバイスの状態を安全に保持するには、クラスのインストーラーや共同インストーラーする必要があります、状態情報を保存、デバイスの内のプロパティとして*ドライバー キー*レジストリにします。 これを行うには、次の手順に従います。

1.  ドライバーのキーを識別するレジストリのハンドルを取得する、*デバイス インスタンス*を使用して、 [ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)で、 *KeyType*パラメーターDIREG_DRV に設定します。

2.  使用[ **SetupDiGetDevicePropertyKeys** ](https://msdn.microsoft.com/library/windows/hardware/ff551965) (デバイスのインスタンスのすべてのプロパティのキーを取得) するまたは[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)(指定したデバイス インスタンス プロパティのキーを取得する) にします。

3.  使用[ **SetupDiSetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552163)デバイス インスタンスのプロパティのキーを保存します。

## <a name="loading-executable-or-dll-files"></a>実行可能ファイルまたは DLL ファイルの読み込み


場合、*共同インストーラー* Windows 64 ビット プラットフォーム、オペレーティング システムで、署名されていない実行可能ファイルまたは DLL を読み込むようにしようからこのセキュリティで保護された環境に読み込まれるようにします。

安全に、クラスのインストーラー ファイルまたは共同インストーラーによって、実行可能ファイルまたは DLL を読み込み、強くお勧め、実行可能ファイルまたは DLL が含まれることで、デジタル署名された[ドライバー パッケージ](driver-packages.md)します。 ドライバー パッケージに署名する方法の詳細については、[ドライバーの署名](driver-signing.md)を参照してください。

**注**  クラスのインストーラーと共同インストーラー読み込む必要がありますいない DLL モジュール明示的な関数の呼び出しによってなど**LoadLibrary**、または依存関係のリンクを作成しています。

 

## <a name="starting-other-processes-or-services"></a>他のプロセスやサービスを開始


デバイスのインストール中には、Windows は追加のプロセスを追跡することはできず、行っているかは終了ときを判断できません。 たとえば、Windows でしたまたは開始または停止、デバイス、プロセスの重要な動作が実行中にシステムの再起動を開始します。

ほとんどの場合、 *co-installer*他のプロセスまたはサービスを開始する必要があります。 、インストーラーを開始できます他のプロセスに安全に呼び出すことによって[CreateProcess](https://go.microsoft.com/fwlink/p/?linkid=194524)関数またはを通じて表示されるダイアログから、[完了-インストール アクション](finish-install-actions--windows-vista-and-later-.md)します。 インストーラーは、作成されたプロセスが終了するまで、ダイアログまたはプロシージャに引き続きユーザーをできないする必要があります。

 

 





