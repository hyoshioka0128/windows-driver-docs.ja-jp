---
title: WMI ドライバーのサポートをテストするための一般的な手法
description: WMI ドライバーのサポートをテストするための一般的な手法
ms.assetid: 4d1a9198-2cc7-491d-a803-80f846882a6e
keywords:
- WMI WDK カーネル、テスト
- WMI のテストサポート WDK カーネル
- WMI WDM プロバイダーが WDK をログに記録する
- エラー WDK WMI
- プロバイダーログ WDK WMI
- イベント WDK WMI
- WMI WDK カーネル、エラー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aff029db061d387d185e198c99d4581ab517ad9
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242913"
---
# <a name="general-techniques-for-testing-wmi-driver-support"></a>WMI ドライバーのサポートをテストするための一般的な手法





### <a name="wmi-client-tools"></a>WMI クライアントツール

ドライバーで WMI サポートをテストするために使用できるツールがいくつかあります。

<a href="" id="wbemtest"></a>Wbemtest  
オペレーティングシステムには、Wbemtest ツールが用意されています。このツールを使用すると、WMI クラスとクラスインスタンスの照会、プロパティ値の変更、メソッドの実行、およびイベント通知の受信を行うことができます。 "Root\\wmi" 名前空間に接続して、ドライバーのサポートをテストします。

<a href="" id="wmic"></a>Wmic.exe  
Microsoft Windows XP 以降のオペレーティングシステムには、WMI 関連のコマンドを発行してドライバーをテストするために使用できるコマンドシェルを提供する Wmic ツールが含まれています。

<a href="" id="wmimofck"></a>Wmimofck  
**Wmimofck**コマンドを使用して、バイナリ MOF ファイルの構文を確認できます。 **Wmimofck**コマンドを使用して、VBScript ファイルを生成することもできます。 このスクリプトを使用すると、ドライバーの WMI クラスインスタンスクエリの処理をテストできます。 **Wmimofck**コマンドを実行すると、web ページが生成され、クエリを実行したり、クラスを設定したり、メソッドを実行したり、イベントを受信したりすることができます。 Web ページでは、複合パラメーターまたは戻り値 (埋め込みクラスの配列など) を使用するメソッドの実行はサポートされていないことに注意してください。 このような場合は、代わりに Wbemtest を使用できます。 Wmimofck の詳細については、「 [wmimofck の使用](using-wmimofck-exe.md)」を参照してください。

また、WMI ユーザーモード API を使用して、カスタム WMI クライアントアプリケーションを作成することによって、ドライバーの WMI サポートをテストすることもできます。

アプリケーションが WMI 情報を提供または使用できるようにする、このユーザーモード API の詳細については、Microsoft Windows SDK のドキュメントの Windows Management Instrumentation に関する情報を参照してください。

WMI クライアントアプリケーションは、次のタスクを実行してドライバーをテストします。

-   WMI に接続します。

    WMI に接続するために、アプリケーションはコンポーネントオブジェクトモデル (COM) 関数**CoCreateInstance**を呼び出して、 **IWbemLocator**インターフェイスへのポインターを取得できます。 次に、アプリケーションは**IWbemLocator:: ConnectServer**メソッドを呼び出して、WMI に接続します。 この呼び出しから、アプリケーションは**IWbemServices**インターフェイスへのポインターを受け取ります。

-   ドライバー内の情報にアクセスします。

    情報にアクセスし、イベントに登録するには、アプリケーションで**IWbemServices**インターフェイスのメソッドを使用します。

### <a href="" id="ddk-wmi-irps-and-the-system-event-log-kg"></a>WMI Irp とシステムイベントログ

厳密にカーネルモードで発生した WMI エラーは、システムイベントログに記録されます。 イベントビューアーを使用して、システムイベントログを調べることができます。 (詳細については、「[ログエラー](logging-errors.md) 」を参照してください)。

このようなエラーの2つの主要な原因は、WMI 要求への不適切な応答と、イベント通知への正しくないパラメーターです。 たとえば、 [**irp\_が\_reginfo**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[**irp\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)によって出力されたときに、ドライバーが間違った形式の[**wmi reginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)データ構造を返した場合、システムイベントログに記録されます。 また、WMI イベント通知を発行するために、 [**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)および[**WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent)への無効な呼び出しもログに記録されます。

### <a href="" id="ddk-wmi-wdm-provider-log-kg"></a>WMI WDM プロバイダーログ

Wmi WDM プロバイダー (Wmiprov) による処理中に発生した WMI エラーは、WMI WDM プロバイダー Wmiprov のログファイルに記録されます。 このテキストファイルは、% windir%\\system32\\wbem\\logs\\wmiprov にあります。 ドライバーの MOF リソースが正しくない、または見つからないなどのエラーがここに記録されます。 無効な MOF リソースの場合、ファイル% windir%\\system32\\mofcomp.exe に、エラーに関する追加情報が含まれている可能性があります。

Windows Vista より前のバージョンの Windows では、Wmimgmt .msc アプリケーションを使用して、すべての WMI プロバイダーのログ設定を変更できます。 (Windows 98/Me では、代わりに Wbemcntl を使用してください)。ログ記録を無効または有効にしたり、WMI ログファイルを保持するディレクトリを変更したりできます。また、このようなファイルの最大サイズを設定することもできます。 詳細については、「 [WMI ログファイル](https://docs.microsoft.com/windows/desktop/WmiSdk/wmi-log-files)」を参照してください。

 

 




