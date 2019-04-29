---
title: トースター ドライバーのサンプルのプログラミング ツアー
description: このトピックでは、学習目的用に設計されたカーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) ドライバーを含むトースター サンプルのコード チュートリアルを提供します。
ms.assetid: 5977AC09-AB53-4CA4-A35A-0E5A1FEE936F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23706c4a4736d6911f3369ba062cbb1ceae8fe92
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325160"
---
# <a name="sample-toaster-driver-programming-tour"></a>トースター ドライバーのサンプルのプログラミング ツアー


このトピックでは、コードのチュートリアルの[トースター](https://go.microsoft.com/fwlink/p/?LinkId=618939)サンプルは、学習目的に設計されたカーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) のドライバーが含まれています。

## <a name="class-installer-and-coinstaller"></a>クラスのインストーラーとの共同インストーラー


Tostrcls プロジェクトでは、クラスのインストーラー DLL を記述する方法を示します。 この DLL は、トースター クラスとカスタム プロパティ シートでカスタム アイコンを提供**デバイス マネージャー**デバイスのフレンドリ名を変更します。 この DLL は、トースター用の INF ファイルで参照されます。

Tostrco1 プロジェクトでは、共同インストーラー DLL を記述する方法を示します。 この DLL は、INF ファイルでカスタム セクションを解析する方法と、デバイスのインスタンス番号に基づいてフレンドリ名を作成する方法を示しています。 この DLL は、トースター用の INF ファイルで参照されます。

## <a name="applications"></a>アプリケーション


このサンプルには、トースター バス ドライバーと関数のドライバーと対話するアプリケーションが含まれています。 これらのアプリケーションは、KMDF と UMDF の両方のトースター バージョンで動作します。

-   Enum.exe は、ユーザー モードの列挙子、簡単なコンソール アプリケーションです。 トースター バスは、物理バスではないために、バス ドライバーのプラグ イン、取り外すと、およびデバイスをシステムから取り出すさせる場合に、このアプリケーションを使用することができます。 使用状況に関するヒントについては、Enum.exe を入力します。
-   Toast.exe:これは、トースターを制御するユーザー モードのコンソール アプリケーションです。 このアプリケーションは、最後の列挙されたデバイスが表示されます、および読み取り要求を送信するトースター デバイスを列挙します。
-   Notify.exe:この GUI アプリケーションでは、Enum.exe と toast.exe の機能を結合し、ユーザー モードでの PnP 通知を処理する方法についても説明します。 たとえば、toastco.inf を使用して、トースターの共同インストーラーをインストールし、PnP 通知を表示するこのアプリを使用します。 関数のドライバーとして読み込まれる別のドライバーが (既定のトースター デバイス ID) 以外の別のハードウェア ID を指定するのに Notify.exe を使用することもできます。

## <a name="kmdf-bus-driver"></a>KMDF バス ドライバー


KMDF バス ドライバーは、トースター バス コント ローラーのサービス、では、接続されているデバイスを列挙し、bus レベルの電源管理を実行します。 バス ドライバーの D0 および D3 をサポートする電源状態。 WMI インターフェイスもあります。 このディレクトリには、トースター バス ドライバーの 2 つの異なる実装を示す 2 つのサブディレクトリが含まれています。

- **静的**

  バス ドライバーの静的なバージョンでは、静的な子リスト、フレームワークによって提供されるデバイスごとに 1 つを使用して子デバイスを列挙する方法を示します。

  *列挙体の静的*を検出し、システムの構成に後続の変更を報告する機能が制限を使用した初期化中に、デバイスの存在をレポートするためのドライバーを使用します。

  バス ドライバーは、デバイスまたは機能のサブユニットの種類と数が事前に定義されたと永続的なおよびドライバーが実行されているシステムの構成に依存しない場合、静的列挙型を使用できます。

  たとえば、サウンド カードのドライバーは、バス ドライバーとして機能し、カードのジョイスティックや MIDI、オーディオなどの機能ごとに個別の物理デバイス オブジェクト (Pdo) を作成します。

  子、バス ドライバーを列挙します。

  1.  呼び出し[ **WdfPdoInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff548786)を取得する、 [WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体。

  2.  初期化します、 [WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体。

  3.  呼び出す[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926) PDO を表す framework デバイス オブジェクトを作成します。

  呼び出した後[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)、ドライバー呼び出し[ **WdfFdoAddStaticChild** ](https://msdn.microsoft.com/library/windows/hardware/ff547225)子デバイスを子リストに追加します。

  ドライバーを使用する必要がありますのみため、あらかじめ決定されているデバイスの構成に関する静的な子の一覧で、永続的なドライバー通常変更を行わない静的子リスト作成した後。 ドライバーを呼び出すことができる場合、ドライバーは、子デバイスがアクセス不能になったことを決定します、 [ **WdfPdoMarkMissing**](https://msdn.microsoft.com/library/windows/hardware/ff548809)します。 (子デバイスがアクセスできるが、応答していない場合は、ドライバーを設定する必要があります、 **Failed**のメンバー、 [ **WDF\_デバイス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff551284)構造体**WdfTrue**を呼び出して[ **WdfDeviceSetDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff546884))。

  バス ドライバーが起動するたびに子デバイスを静的に列挙するために、トースター バス ドライバーのデバイス パラメーターのキーのレジストリ値を設定できます。

  **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\Enum\\ルート\\システム\\&lt;インスタンス番号&gt;\\デバイス パラメーター**

  **NumberOfToasters:REG\_DWORD:2 で失敗する**

  このレジストリ設定を使用して列挙子のデバイスの最大数には 10 です。 トースター Bus Inf ファイルでこの値を構成することもできます。

- **動的**

  動的バス ドライバーのバージョンでは、オブジェクトの一覧を列挙子を使用して子デバイス方法を示します。

  *動的な列挙*を検出し、システムの実行中に、システムに接続されているデバイスの種類と数に変更を報告するためのドライバーを使用します。

  バス ドライバーは、数または親デバイスに接続されているデバイスの種類はシステムの構成に依存している場合、動的な列挙型を使用する必要があります。 これらのデバイスの一部のシステムに常に接続する可能性があり、いくつかに接続されているし、システムの実行中に電源が入っていない可能性があります。

  たとえば、システムの PCI バスに接続されているデバイスの種類と数がシステムに依存するが、ユーザー電源をオフに、開く場合とを追加しますかドライバーを使用してデバイスを削除しない限り、永続的なは。 その一方で、ユーザーは追加または取り外しを行うシステムの実行中に、ケーブルを取り外すして USB デバイスを削除できます。

  バス ドライバーが、子デバイスを識別するたびに子リストに子デバイスの説明を追加する必要があります、します。 ドライバーを呼び出してフレームワークが提供するデバイスの既定の子のリストを使用できますか[ **WdfFdoGetDefaultChildList**](https://msdn.microsoft.com/library/windows/hardware/ff547235)、リストを作成できます追加の子をグループ化の子を呼び出すことによって、または[**WdfChildListCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545615)します。 このサンプルでは、既定の子リストを使用します。 A*子説明*は、必須の*識別説明*は省略可能*説明に対処*。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">用語</th>
  <th align="left">説明</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><a href="" id="---------------------identification-description"></a> 識別の説明</p></td>
  <td align="left"><p>識別の説明は、ドライバーを列挙する各デバイスを一意に識別する情報を含む構造です。 ドライバーは、この構造体を定義しますが、その最初のメンバーである必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551223" data-raw-source="[&lt;strong&gt;WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551223)"> <strong>WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER</strong> </a>構造体。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="" id="---------------------address-description"></a> アドレスの説明</p></td>
  <td align="left"><p>アドレスの説明は、デバイスが接続中に情報を変更できる場合、そのバス上のデバイスにアクセスできるようにをドライバーが必要な情報を格納する構造体です。 ドライバーは、この構造体を定義しますが、その最初のメンバーである必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551223" data-raw-source="[&lt;strong&gt;WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551223)"> <strong>WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER</strong> </a>構造体。 アドレスの説明は省略可能です。 このサンプルでは、アドレスの説明は使用しません。</p></td>
  </tr>
  </tbody>
  </table>




子の一覧では、ドライバーの呼び出しに子を追加する[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)検出された各子デバイス。 この呼び出しは、ドライバーが、親デバイスに接続されている子デバイスを検出されたことをフレームワークに通知します。 ドライバーを呼び出すと**WdfChildListAddOrUpdateChildDescriptionAsPresent**識別の説明と、必要に応じて、アドレスの説明を提供します。

ドライバーの呼び出し後[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)フレームワークを新しいデバイスを報告するには、新しいデバイスに存在する PnP マネージャーに通知します。 PnP マネージャーは、デバイス スタックと新しいデバイスのドライバー スタックを作成します。 このプロセスの一環として、フレームワークに呼び出す、バス ドライバーの[ *EvtChildListCreateDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540828)コールバック関数。 このコールバック関数を呼び出す必要があります[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)を新しいデバイスの PDO を作成します。

不足している子デバイスを報告するには、このドライバーは WdfChildListUpdateChildDescriptionAsMissing を呼び出します。 動的な列挙型の詳細については、framework のドキュメントを参照してください。


## <a name="kmdf-function-driver"></a>KMDF 関数ドライバー


関数のドライバーには、2 つの異なるバージョンが含まれている: wdfsimple wdffeatured とします。 2 つの関数のドライバーのバージョンで共通のヘッダー ファイルの共有、*共有*ディレクトリ。

-   **WdfSimple**

    このバージョンでは、ドライバーは、PnP、電源イベントを処理しないし、これらのイベントのフレームワークの既定のサポートを代わりに依存します。 Notify.exe などのアプリケーションは、このドライバーを使用して、ドライバーによって登録されたデバイスのインターフェイスを開くし、読み取り、書き込み、または IOCTL 要求を送信します。

-   **WdfFeatured**

    このバージョンの PNP、電源イベントが登録を処理する方法を示しています。 作成とファイル要求を閉じる、WMI セットの処理と、イベントをクエリおよび WMI 通知イベントをトリガーします。 電源ポリシーの所有者であるにも登録アイドル状態の通知の I/O アクティビティがない場合、デバイスを低電力状態に配置できるようにします。

## <a name="kmdf-filter-driver"></a>KMDF フィルター ドライバー


このディレクトリには、2 つのフィルター ドライバーのソース コードが含まれています。 汎用のサンプルは、単純なパススルー フィルター ドライバーです。 側波帯は、制御デバイス オブジェクトを使用して、アプリケーションに側波帯 ioctl インターフェイスを提供する方法を示します。 このプライベート インターフェイスでは、直接フィルター ドライバーと対話するアプリケーションを使用できます。を接続をフィルター処理する機能のデバイス スタックはバイパスされます。 側波帯サンプルでは、ドライバーは、1 つ以上のデバイスの要求を処理する場合は、デバイス オブジェクトのコレクションを実装する方法も示します。 これらのフィルターは、filter.inf を使用してトースターの既存のデバイスにインストールできます。

## <a name="kmdf-toastmon"></a>KMDF Toastmon


このサンプルでは、デバイスを開くし、リモートの I/O ターゲット インターフェイスを使用してカーネル モードで I/O を実行する方法を示します。 このサンプルでは、呼び出すことによって、トースター インターフェイス クラスの PnP 通知コールバック ルーチンを登録します。 [ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)します。 トースター デバイスを接続、PnP マネージャーは、コールバックを呼び出します。 コールバックは、このサンプルは、リモート ターゲットを作成し、コールバックのデータで提供されるシンボリック リンクを使用して、デバイスを開きます。

また、このサンプルでは、非同期読み取りを示し、ターゲット デバイスへの書き込みにパッシブ タイマーを使用します。 登録することによって、デバイスの変更通知に応答する方法も示します[ *EvtIoTargetQueryRemove*](https://msdn.microsoft.com/library/windows/hardware/ff541793)/[*EvtIoTargetRemoveCanceled* ](https://msdn.microsoft.com/library/windows/hardware/ff541800) / [ *EvtIoTargetRemoveComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff541806) I/O ターゲット オブジェクト。 ドライバーは、ドライバーを制御していない別のデバイスと通信する場合は、この手法を使用できます。 Wdftoastmon.inf を使用して、ルート列挙デバイスとしては、このドライバーをインストールします。 トースター バス ドライバーのインストールのと同じ手順を使用します。

## <a name="umdf-function-driver"></a>UMDF 関数ドライバー


WUDFToaster ドライバーでは、ドライバーによって登録されているデバイスのインターフェイスを開き、読み取り、書き込み、または IOCTL 要求を送信するユーザー アプリケーション (toast/notify.exe) を使用します。 このドライバーのサンプルでは、PnP と電力のイベントの登録、電源ポリシーの所有権を設定および I/O 要求を処理する方法も示します。 これは、実稼働環境での使用を目的としない最小限のドライバーのサンプルです。

KMDF Toastmon サンプルと組み合わせて WUDF トースターを使用すると、リモートの I/O ターゲットを使用してユーザー モード ドライバーにカーネル モードのクライアント アクセスを示します。

これを行うには、次の行を追加します。UMDF ドライバーの INF の WDF セクション:**UmdfKernelModeClientPolicy AllowKernelModeClients を =**

### <a name="testing-umdf-toaster"></a>UMDF トースターのテスト

1.  Toast.exe、Notify.exe または Enum.exe アプリケーションを使用します。
2.  KMDF Toastmon ドライバーをインストールします。 前述のように、ユーザー モード ドライバーにカーネル モードのクライアントを許可します。 WUDFToaster.dll をインストールします。 Traceview.exe を使用して、UMDF トースターに Toastmon から送信された要求を参照してください。

### <a href="" id="umdf-toastmon"></a>UMDF Toastmon の概要

このサンプルは、KMDF ToastMon サンプルの UMDF バージョンです。

UMDF Toastmon は UMDF を使用して、ユーザー モード ドライバー フレームワークと最小限のドライバーを作成する方法について説明し、ベスト プラクティスを示します。 ドライバーは、(ルート列挙または実際のハードウェア デバイス) のデバイスで正常に読み込まれますが最低限の PnP 機能し、I/O 操作の受信をサポートしていません。

Toastmon は、記述することが他の UMDF ドライバーの学習ツールとして使用するためのものです。









