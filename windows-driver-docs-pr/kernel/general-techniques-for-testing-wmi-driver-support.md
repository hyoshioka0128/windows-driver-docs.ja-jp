---
title: WMI ドライバーのサポートをテストするための一般的な手法
description: WMI ドライバーのサポートをテストするための一般的な手法
ms.assetid: 4d1a9198-2cc7-491d-a803-80f846882a6e
keywords:
- WMI の WDK のカーネルのテスト
- WMI のサポートの WDK カーネルのテスト
- WMI WDM プロバイダー ログ WDK
- WDK WMI エラー
- WDK の WMI プロバイダーをログします。
- WDK の WMI イベント
- WMI の WDK カーネルでは、エラー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9735c59323a45ddd39855aff8593b97c19688452
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386591"
---
# <a name="general-techniques-for-testing-wmi-driver-support"></a>WMI ドライバーのサポートをテストするための一般的な手法





### <a name="wmi-client-tools"></a>WMI クライアント ツール

ドライバーで WMI のサポートをテストする際のいくつかのツールがあります。

<a href="" id="wbemtest"></a>Wbemtest  
オペレーティング システムには、WMI クラスとクラスのインスタンスに対してクエリを実行、プロパティ値を変更、execute メソッド、およびイベント通知を受信する際の GUI を提供する Wbemtest ツールが含まれています。 接続、"ルート\\wmi"ドライバーのサポートをテストする名前空間。

<a href="" id="wmic"></a>Wmic  
Microsoft Windows XP およびそれ以降のオペレーティング システム、ドライバーをテストする WMI 関連のコマンドを発行する際のコマンド シェルを提供する Wmic ツールが含まれます。

<a href="" id="wmimofck"></a>Wmimofck  
**Wmimofck**コマンドを使用して、バイナリの MOF ファイルの構文を確認できます。 使用することも、 **wmimofck t** VBScript ファイルを生成するコマンド。 このスクリプトを使用すると、WMI クラスのインスタンスのクエリのドライバーの処理をテストします。 **Wmimofck-w**コマンドには、クエリを実行およびクラスを設定、メソッドを実行し、イベントの受信をテストする web ページが生成されます。 Web ページは、複雑なパラメーターを使用して、または戻り値 (埋め込まれたクラスの配列) などを実行中のメソッドをサポートされていないことに注意してください。 このような場合は、Wbemtest を代わりに使用することができます。 参照してください[wmimofck.exe を使用して](using-wmimofck-exe.md)Wmimofck の詳細についてはします。

テストすることもドライバーの WMI のサポートするカスタムの WMI クライアント アプリケーションを記述することで、WMI のユーザー モード API を使用します。

提供または WMI 情報を使用するアプリケーションでは、このユーザー モード API の詳細については、Windows Management Instrumentation については、Microsoft Windows SDK ドキュメントを参照してください。

WMI クライアント アプリケーションは、ドライバーをテストする次のタスクを実行します。

-   WMI に接続します。

    WMI に接続するには、アプリケーションが、コンポーネント オブジェクト モデル (COM) 関数を呼び出すことができます**CoCreateInstance**へのポインターを取得する、**セグ: 前**インターフェイス。 その後、アプリケーションを呼び出す、 **IWbemLocator::ConnectServer** WMI に接続するメソッド。 アプリケーション、この呼び出しからへのポインターが受信、 **IWbemServices**インターフェイス。

-   ドライバーの情報にアクセスします。

    情報にアクセスして、イベントを登録するには、アプリケーションがのメソッドを使用して、 **IWbemServices**インターフェイス。

### <a href="" id="ddk-wmi-irps-and-the-system-event-log-kg"></a>WMI の Irp およびシステム イベント ログ

カーネル モードで厳密に発生する WMI エラーは、システム イベント ログに記録されます。 イベント ビューアーを使用すると、システム イベント ログを確認します。 (を参照してください[ログ エラー](logging-errors.md)詳細についてはします)。

このようなエラーの 2 つの主要なソース WMI 要求への形式が正しくない応答、イベント通知に不正確なパラメーターです。 たとえば、ドライバーは、正しくない形式を返します[ **WMIREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmireginfow)への応答内のデータ構造、 [ **IRP\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[ **IRP\_MN\_REGINFO\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)要求、システムはをシステム イベント ログに記録されます。 システムに無効な呼び出しを記録しても[ **IoWMIWriteEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiwriteevent)と[ **WmiFireEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmifireevent) WMI イベント通知を発行します。

### <a href="" id="ddk-wmi-wdm-provider-log-kg"></a>WMI WDM プロバイダー ログ

WMI WDM プロバイダー (Wmiprov.dll) によって処理される際に発生する WMI エラーは、WMI WDM プロバイダー、Wmiprov.log のログ ファイルに記録されます。 これは、テキスト ファイルを %windir% で見つかります\\system32\\wbem\\ログ\\wmiprov.log します。 ここで、ドライバーの正しくないか、不足している MOF リソースなどのエラーが記録されます。 場合は、次のように不適切な MOF リソース ファイル %windir%\\system32\\mofcomp.log がエラーに関連する追加の情報を必要があります。

Windows Vista より前のバージョンの Windows では、Wmimgmt.msc アプリケーションを使用してすべての WMI プロバイダーのログ設定を変更できます。 (Windows 98/Wbemcntl を代わりに、使用します)。無効にする、ログ記録を再度有効にまたは、ディレクトリ、WMI のログ ファイルは、保持だけでなくこのようなファイルの最大サイズの設定を変更できます。 詳細については、次を参照してください。 [WMI ログファイル](https://docs.microsoft.com/windows/desktop/WmiSdk/wmi-log-files)します。

 

 




