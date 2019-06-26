---
title: DIF コードの処理
description: DIF コードの処理
ms.assetid: cb54bc04-4cd4-4eec-ad74-2abbf601de54
keywords:
- 差分のコードの共同インストーラー WDK デバイス インストール
- 差分コード WDK デバイスのインストール
- デバイス インストールの関数コード WDK
- 関数コードの WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45ec8f1f7e3d9a97af11f835102d0b614149263f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383847"
---
# <a name="handling-dif-codes"></a>DIF コードの処理





*デバイスのインストール アプリケーション*送信[デバイス インストールの関数コード](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))(差分コード) を呼び出すことによってインストーラー [ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller). この関数は、インストーラーのエントリ ポイント関数を呼び出します。 インストーラーのエントリ ポイントの説明を参照してください。

[共同インストーラー インターフェイス](co-installer-interface.md)

差分の各コードのリファレンス ページには、次のセクションが含まれています。

<a href="" id="when-sent"></a>**送信されたときに**  
時間、およびデバイスのインストール アプリケーションがこの差分要求を送信する理由は、上の理由から、一般的なについて説明します。

<a href="" id="who-handles"></a>**処理します。**  
この要求を処理するためにどのインストーラーが許可されているを指定します。 インストーラーには、クラスのインストーラー、クラスの共同インストーラー (セットアップ クラス全体の共同インストーラー)、およびデバイスの共同インストーラーが含まれます (共同インストーラーをデバイスに固有)。

<a href="" id="installer-input"></a>**インストーラーの入力**  
差分のコードだけでなく**SetupDiCallClassInstaller**特定の要求に関連する追加の情報を提供します。 各要求で提供される情報の詳細については、各差分コードのリファレンス ページを参照してください。 次の一覧は、追加の入力パラメーターの一般的な説明が含まれていて、一覧表示、[デバイスのインストール機能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))(**SetupDi * Xxx*** 関数) インストーラーは、処理するために呼び出すことができます、パラメーター:

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
装置のデバイス情報へのハンドルを設定します。

ハンドルが非透過的です。 ハンドルを使用して、たとえば、デバイス情報を識別する呼び出しで設定**SetupDi * Xxx*** 関数。

*DeviceInfoSet* 、関連付けられている必要があります[デバイス セットアップ クラス](device-setup-classes.md)します。 そうである場合は、呼び出す[ **SetupDiGetDeviceInfoListClass** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinfolistclass)クラス GUID を取得します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
必要に応じてへのポインターを提供、 [ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)デバイス情報のセット内のデバイスを識別する構造体。

<a href="" id="device-installation-parameters-"></a>*デバイスのインストール パラメーター*   
これらの間接的なパラメーターは、デバイスのインストールでの情報を提供する[ **SP_DEVINSTALL_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)構造体。 場合*DeviceInfoData*ない**NULL**、インストールのパラメーターに関連付けられているデバイスがある、 *DeviceInfoData*します。 場合*DeviceInfoData*は**NULL**、関連付けられているデバイスのインストール パラメーター、 *DeviceInfoSet*します。

呼び出す[ **SetupDiGetDeviceInstallParams** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstallparamsa)デバイスのインストール パラメーターを取得します。

<a href="" id="class-installation-parameters"></a>*インストール パラメーターをクラスします。*  
省略可能な間接的なパラメーターは、特定の差分要求に固有です。 これらは基本的に「差分要求パラメーターです」 たとえば、DIF_REMOVE インストール要求のクラスのインストール パラメーターは、SP_REMOVEDEVICE_PARAMS 構造体に格納されます。

各 sp _*XXX*_PARAMS 構造 SP_CLASSINSTALL_HEADER 固定サイズ構造体から始まります。

呼び出す[ **SetupDiGetClassInstallParams** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassinstallparamsa)クラス インストール パラメーターを取得します。

差分要求がクラスのインストール パラメーターを持つ場合は、一連のパラメーターに関連付けられている、 *DeviceInfoSet*と別のセットに関連付けられているパラメーターの*DeviceInfoData* (差分を要求した場合指定します*DeviceInfoData*)。 **SetupDiGetClassInstallParams**使用可能な最も固有のパラメーターを返します。

<a href="" id="context"></a>*コンテキスト*  
共同インストーラーは、省略可能なコンテキスト パラメーターを指定します。

<a href="" id="installer-output"></a>**インストーラーの出力**  
この差分コードに必要な出力をについて説明します。

インストーラーでは、デバイスのインストール パラメーターを変更する場合、インストーラーを呼び出す必要があります[ **SetupDiSetDeviceInstallParams** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa)を返す前に、変更を適用します。 同様に、インストーラーが差分コードのクラスのインストール パラメーターを変更した場合、インストーラー呼び出す必要があります[ **SetupDiSetClassInstallParams**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassinstallparamsa)します。

<a href="" id="installer-return-value"></a>**インストーラーの戻り値**  
適切なリターン DIF コードの値を指定します。 戻り値の詳細については、次の図を参照してください。

<a href="" id="default-dif-code-handler"></a>**既定の差分コード ハンドラー**  
指定します、 **SetupDi * Xxx*** DIF コードのシステム定義の既定の操作を実行する関数。 差分のすべてのコードでは、既定のハンドラーがあります。 共同インストーラーまたはクラスのインストーラーは、既定のハンドラーが呼び出されることを防ぐために手順を実行しない限り、 **SetupDiCallClassInstaller**クラスのインストーラーが呼び出された後 (ただし、いずれかを呼び出す前に、差分コードの既定のハンドラーを呼び出します共同インストーラー処理後に登録されている)。

クラスのインストーラーが正常に差分コードを処理する場合と**SetupDiCallClassInstaller**既定のハンドラーを呼び出す必要があります、その後、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

クラスのインストーラーが正常に差分コードは、既定のハンドラーを直接呼び出しなどを処理する場合、クラスのインストーラーは NO_ERROR を返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しはもう一度です。 クラスのインストーラーは、既定のハンドラーを直接呼び出すことができますが、クラスのインストーラーは、既定のハンドラーの操作を優先することはありません試みる必要があることに注意してください。

クラスのインストーラーには、エラーが発生すると、インストーラーが適切な Win32 エラー コードを返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しは。

共同インストーラーが*いない*既定 DIF コード ハンドラーを呼び出します。

<a href="" id="installer-operation"></a>**インストーラーの操作**  
インストーラーは、差分の要求を処理するためにかかる可能性がある一般的な手順について説明します。

<a href="" id="see-also"></a>**参照してください。**  
関連情報のソースを一覧表示されます。

次の図は、シーケンス内のイベントの**SetupDiCallClassInstaller** DIF コードを処理するためです。

![setupdicallclassinstaller で処理する差分コードのフローを示す図](images/dif-flow.png)

オペレーティング システムでは、各差分コードのいくつかの操作を実行します。 ベンダーから提供された共同インストーラーおよびクラスのインストーラーは、インストール操作に参加できます。 なお**SetupDiCallClassInstaller**処理後の差分コードが失敗した場合でも登録されている共同インストーラーを呼び出します。

 

 





