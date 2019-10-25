---
title: トースター ドライバーのサンプルのプログラミング ツアー
description: このトピックでは、トースターサンプルのコードチュートリアルを提供します。このサンプルには、学習用に設計されたカーネルモードドライバーフレームワーク (KMDF) とユーザーモードドライバーフレームワーク (UMDF) ドライバーが含まれています。
ms.assetid: 5977AC09-AB53-4CA4-A35A-0E5A1FEE936F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a248f805a01d025eed0262160b68c5151f3c7ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842196"
---
# <a name="sample-toaster-driver-programming-tour"></a>トースター ドライバーのサンプルのプログラミング ツアー


このトピックでは、[トースター](https://go.microsoft.com/fwlink/p/?LinkId=618939)サンプルのコードチュートリアルを提供します。このサンプルには、学習用に設計されたカーネルモードドライバーフレームワーク (kmdf) とユーザーモードドライバーフレームワーク (UMDF) ドライバーが含まれています。

## <a name="class-installer-and-coinstaller"></a>クラスインストーラーと共同インストーラー


Tostrcls プロジェクトは、クラスインストーラー DLL を記述する方法を示しています。 この DLL は、トースタークラスのカスタムアイコンと、デバイスのフレンドリ名を変更するための**デバイスマネージャー**のカスタムプロパティシートを提供します。 この DLL は、トースターの INF ファイルで参照されています。

Tostrco1 プロジェクトは、共同作成 DLL を記述する方法を示しています。 この DLL は、デバイスのインスタンス番号に基づいてフレンドリ名を作成する方法、および INF ファイルのカスタムセクションを解析する方法を示しています。 この DLL は、トースターの INF ファイルで参照されています。

## <a name="applications"></a>アプリケーション


このサンプルには、トースター bus ドライバーおよび関数ドライバーと対話するアプリケーションが含まれています。 これらのアプリケーションは、KMDF と UMDF トースターの両方のバージョンで動作します。

-   列挙型は、単純なコンソールアプリケーションであるユーザーモードの列挙子です。 トースター bus は物理バスではないため、このアプリケーションを使用して、バスドライバーがシステムからデバイスを接続し、取り外し、取り外しを行うことができます。 使用方法のヒントについては、「System.enum」と入力してください。
-   トースト: これは、トースターを制御するためのユーザーモードのコンソールアプリケーションです。 このアプリケーションは、トースターデバイスを列挙し、最後に列挙されたデバイスを開き、そのデバイスに読み取り要求を送信します。
-   Notification .exe: この GUI アプリケーションは、列挙型 .exe とトースト .exe の機能を組み合わせたもので、ユーザーモードでの PnP 通知の処理方法も示しています。 たとえば、toastco を使用してトースターの共同インストーラーをインストールし、このアプリを使用して PnP 通知を表示します。 また、通知を使用して別のハードウェア ID (既定のトースターデバイス ID 以外) を指定すると、別のドライバーを関数ドライバーとして読み込むことができます。

## <a name="kmdf-bus-driver"></a>KMDF バスドライバー


KMDF バスドライバーは、トースター bus コントローラーをサービスし、接続されているデバイスを列挙し、バスレベルの電源管理を実行します。 バスドライバーは、D0 および D3 の電源状態をサポートしています。 また、WMI インターフェイスもあります。 このディレクトリには、トースター bus ドライバーの2つの異なる実装を示す2つのサブディレクトリが含まれています。

- **雑音**

  静的バージョンのバスドライバーは、フレームワークによって提供される、デバイスごとに1つずつ静的な子リストを使用して、子デバイスを列挙する方法を示しています。

  *静的列挙*を使用すると、ドライバーは、初期化中にデバイスの存在を検出して報告することができます。この場合、システムの構成に対するその後の変更を報告する機能は限られています。

  バスドライバーは、デバイスまたは機能サブユニットの数と種類が事前に設定され、永続的であり、ドライバーが実行されているシステムの構成に依存していない場合に、静的な列挙を使用できます。

  たとえば、サウンドカードのドライバーはバスドライバーとして機能し、MIDI、オーディオ、ジョイスティックなどのカードの機能ごとに個別の物理デバイスオブジェクト (PDOs) を作成することができます。

  子を列挙するには、バスドライバーを次のようにします。

  1.  [**Wdfpdoinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)を呼び出して、 [wdfdevice\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体を取得します。

  2.  [Wdfdevice\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体を初期化します。

  3.  [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、PDO を表すフレームワークデバイスオブジェクトを作成します。

  [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出した後、ドライバーは[**Wdffdoaddstaticchild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoaddstaticchild)を呼び出して子デバイスを子リストに追加します。

  ドライバーは、事前に決められた永続的なデバイス構成の静的な子リストのみを使用する必要があるため、通常、ドライバーは、作成後に静的子リストを変更しません。 子デバイスがアクセス不能になったとドライバーが判断した場合、ドライバーは[**Wdfpdomarkmissing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdomarkmissing)を呼び出すことができます。 (子デバイスにアクセスできても応答しない場合、ドライバーは、 [**WDF\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_state)構造の**失敗した**メンバーを**wdftrue**に設定してから、 [**wdfdevicesetdevicestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)を呼び出します)。

  バスドライバーが起動するたびに子デバイスを静的に列挙するために、トースター Bus ドライバーのデバイスパラメーターキーにレジストリ値を設定できます。

  **HKEY\_ローカル\_マシン\\SYSTEM\\CurrentControlSet\\列挙型\\ルート\\システム\\&lt;インスタンス番号&gt;\\デバイスパラメーター**

  **NumberOfToasters: REG\_DWORD: 2**

  このレジストリ設定を使用して列挙できる子デバイスの最大数は10です。 この値は、トースター Bus Inf ファイルを使用して構成することもできます。

- **動的**

  動的バージョンのバスドライバーは、子リストオブジェクトを使用して子デバイスを列挙する方法を示しています。

  *動的列挙*を使用すると、ドライバーは、システムの実行中にシステムに接続されているデバイスの数と種類に対する変更を検出し、報告することができます。

  親デバイスに接続されているデバイスの数または種類がシステムの構成によって異なる場合、バスドライバーは動的列挙を使用する必要があります。 これらのデバイスの中には、常にシステムに接続されているものと、システムの実行中に接続が切断されているものがあります。

  たとえば、システムの PCI バスに接続されているデバイスの数と種類はシステムに依存しますが、ユーザーが電源をオフにした場合は永続的な状態になります。また、ドライバーを使用してデバイスを追加または削除しない限り、永続的になります。 一方、ユーザーは、システムの実行中にケーブルを接続または取り外して、USB デバイスを追加または削除できます。

  バスドライバーが子デバイスを識別するたびに、子デバイスの説明を子リストに追加する必要があります。 ドライバーでは、 [**WdfFdoGetDefaultChildList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdogetdefaultchildlist)を呼び出すことによって、フレームワークに用意されているデバイスの既定の子リストを使用することも、 [**Wdfchildlistcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistcreate)を呼び出して子をグループ化するために追加の子リストを作成することもできます。 このサンプルでは、既定の子リストを使用します。 *子の説明*は、必須の*識別の説明*とオプションのアドレスの*説明*で構成されます。

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
  <td align="left"><p><a href="" id="---------------------identification-description"></a>識別の説明</p></td>
  <td align="left"><p>識別の説明は、ドライバーが列挙する各デバイスを一意に識別する情報を含む構造体です。 ドライバーはこの構造体を定義しますが、その最初のメンバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_identification_description_header" data-raw-source="[&lt;strong&gt;WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_identification_description_header)"><strong>WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER</strong></a>構造体である必要があります。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="" id="---------------------address-description"></a>アドレスの説明</p></td>
  <td align="left"><p>アドレスの説明は、デバイスが接続されている間に情報が変更される可能性がある場合に、バス上のデバイスにアクセスするためにドライバーが必要とする情報を含む構造体です。 ドライバーはこの構造体を定義しますが、その最初のメンバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_identification_description_header" data-raw-source="[&lt;strong&gt;WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_identification_description_header)"><strong>WDF_CHILD_IDENTIFICATION_DESCRIPTION_HEADER</strong></a>構造体である必要があります。 アドレスの説明は省略可能です。 このサンプルでは、アドレスの説明は使用しません。</p></td>
  </tr>
  </tbody>
  </table>




子リストに子を追加するために、ドライバーは、検出された各子デバイスの[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)を呼び出します。 この呼び出しは、親デバイスに接続されている子デバイスがドライバーによって検出されたことをフレームワークに通知します。 ドライバーが**WdfChildListAddOrUpdateChildDescriptionAsPresent**を呼び出すと、id の説明と、必要に応じてアドレスの説明が提供されます。

ドライバーが[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)を呼び出して新しいデバイスを報告した後、新しいデバイスが存在することを PnP マネージャーに通知します。 PnP マネージャーは、新しいデバイスのデバイススタックとドライバースタックを構築します。 このプロセスの一環として、フレームワークはバスドライバーの[*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)コールバック関数を呼び出します。 このコールバック関数は、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、新しいデバイス用の PDO を作成する必要があります。

子デバイスが見つからないことを報告するために、このドライバーは WdfChildListUpdateChildDescriptionAsMissing を呼び出します。 動的列挙の詳細については、フレームワークのドキュメントを参照してください。


## <a name="kmdf-function-driver"></a>KMDF 関数ドライバー


関数ドライバーには、wdfsimple と wdffeatured という2つの異なるバージョンがあります。 2つのバージョンの関数ドライバーは、*共有*ディレクトリに共通のヘッダーファイルを共有します。

-   **WdfSimple**

    このバージョンでは、ドライバーは PnP および電源イベントを処理せず、代わりにこれらのイベントに対するフレームワークの既定のサポートに依存します。 Notify などのアプリケーションは、このドライバーを使用して、ドライバーによって登録されたデバイスインターフェイスを開き、読み取り、書き込み、または IOCTL 要求を送信できます。

-   **WdfFeatured**

    このバージョンでは、PNP と電源イベントに登録する方法、ファイル要求の作成と終了、WMI セットおよびクエリイベントの処理、WMI 通知イベントのトリガーを行う方法を示します。 電源ポリシーの所有者は、アイドル通知も登録します。これにより、i/o アクティビティがないときにデバイスの電源を低状態にすることができます。

## <a name="kmdf-filter-driver"></a>KMDF フィルタードライバー


このディレクトリには、2つのフィルタードライバーのソースコードが含まれています。 汎用サンプルは、単純な passthru フィルタードライバーです。 SideBand は、コントロールデバイスオブジェクトを使用して、SideBand ioctl インターフェイスをアプリケーションに提供する方法を示しています。 このプライベートインターフェイスにより、アプリケーションはフィルタードライバーと直接通信できます。フィルターがアタッチされている機能デバイススタックをバイパスする。 また、SideBand サンプルでは、ドライバーが複数のデバイスの要求を処理する場合に、デバイスオブジェクトのコレクションを実装する方法も示しています。 これらのフィルターは、トースターを使用して既存のデバイスにインストールできます。

## <a name="kmdf-toastmon"></a>KMDF Toastmon


このサンプルでは、リモート i/o ターゲットインターフェイスを使用してデバイスを開き、カーネルモードで i/o を実行する方法を示します。 このサンプルでは、 [**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出して、トースターインターフェイスクラスの PnP 通知コールバックルーチンを登録します。 トースターデバイスが接続されている場合は、PnP マネージャーがコールバックを呼び出します。 このサンプルでは、コールバックでリモートターゲットを作成し、コールバックデータに指定されたシンボリックリンクを使用してデバイスを開きます。

また、このサンプルではパッシブタイマーを使用して、ターゲットデバイスに対する非同期の読み取りと書き込みを示します。 また、i/o ターゲットオブジェクトで[*Evtiotargetqueryremove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)/[*EvtIoTargetRemoveCanceled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)/[*EvtIoTargetRemoveComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)を登録して、デバイス変更通知に応答する方法についても説明します。 ドライバーが制御していない別のデバイスにドライバーが通信する場合は、この手法を使用できます。 このドライバーは、ルートで列挙されたデバイスとして、Wdftoastmon を使用してインストールします。 トースター bus ドライバーと同じ手順をインストールに使用します。

## <a name="umdf-function-driver"></a>UMDF 関数ドライバー


WUDFToaster ドライバーは、ユーザーアプリケーション (トースト/通知 .exe) が、ドライバーによって登録されたデバイスインターフェイスを開き、読み取り、書き込み、または IOCTL 要求を送信できるようにします。 このドライバーサンプルでは、PnP と電源イベントに登録する方法、電源ポリシーの所有権を設定する方法、および i/o 要求を処理する方法も示しています。 これは、実稼働環境での使用を意図していない最小ドライバーサンプルです。

WUDF トースターを KMDF Toastmon サンプルと組み合わせて使用すると、リモート i/o ターゲットを使用するユーザーモードドライバーへのカーネルモードクライアントアクセスを示すことができます。

これを行うには、に次の行を追加します。この UMDF ドライバーの INF の WDF セクション: **Umdfカーネル Modeclientpolicy = allowkernelmodeclients**

### <a name="testing-umdf-toaster"></a>UMDF トースターのテスト

1.  トースト、通知 .exe、または列挙型の .exe アプリケーションを使用します。
2.  KMDF Toastmon ドライバーをインストールします。 前に説明したように、カーネルモードのクライアントにユーザーモードのドライバーを許可します。 WUDFToaster をインストールします。 Traceview .exe を使用して、Toastmon から UMDF トースターに送信された要求を確認します。

### <a href="" id="umdf-toastmon"></a>UMDF Toastmon の概要

このサンプルは、KMDF ToastMon サンプルの UMDF バージョンです。

UMDF Toastmon では、UMDF を使用して、ユーザーモードドライバーフレームワークで最小ドライバーを記述し、ベストプラクティスを示します。 ドライバーはデバイス (ルート列挙型または実際のハードウェアデバイス) に正常に読み込まれますが、最小の PnP 機能があり、i/o 操作の受信をサポートしていません。

Toastmon は、記述できる他の UMDF ドライバーの学習ツールとして機能することを意図しています。









