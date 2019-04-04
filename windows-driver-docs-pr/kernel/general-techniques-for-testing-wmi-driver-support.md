---
title: WMI のドライバーをテストするための一般的な手法をサポートします。
description: WMI のドライバーをテストするための一般的な手法をサポートします。
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
ms.openlocfilehash: 8f6c326a43b9c5dbef7029d6cbb1d382d2590bc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559061"
---
# <a name="general-techniques-for-testing-wmi-driver-support"></a>WMI のドライバーをテストするための一般的な手法をサポートします。





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

このようなエラーの 2 つの主要なソース WMI 要求への形式が正しくない応答、イベント通知に不正確なパラメーターです。 たとえば、ドライバーは、正しくない形式を返します[ **WMIREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565832)への応答内のデータ構造、 [ **IRP\_MN\_REGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff551731)または[ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734)要求、システムはをシステム イベント ログに記録されます。 システムに無効な呼び出しを記録しても[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)と[ **WmiFireEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff565807) WMI イベント通知を発行します。

### <a href="" id="ddk-wmi-wdm-provider-log-kg"></a>WMI WDM プロバイダー ログ

WMI WDM プロバイダー (Wmiprov.dll) によって処理される際に発生する WMI エラーは、WMI WDM プロバイダー、Wmiprov.log のログ ファイルに記録されます。 これは、テキスト ファイルを %windir% で見つかります\\system32\\wbem\\ログ\\wmiprov.log します。 ここで、ドライバーの正しくないか、不足している MOF リソースなどのエラーが記録されます。 場合は、次のように不適切な MOF リソース ファイル %windir%\\system32\\mofcomp.log がエラーに関連する追加の情報を必要があります。

Windows Vista より前のバージョンの Windows では、Wmimgmt.msc アプリケーションを使用してすべての WMI プロバイダーのログ設定を変更できます。 (Windows 98/Wbemcntl を代わりに、使用します)。無効にする、ログ記録を再度有効にまたは、ディレクトリ、WMI のログ ファイルは、保持だけでなくこのようなファイルの最大サイズの設定を変更できます。 詳細については、[WMI ログファイル](https://msdn.microsoft.com/library/aa394564)を参照してください。

 

 




