---
title: UMDF 2 に UMDF 1 からドライバーの移植
description: このトピックでは、UMDF 2 に、ユーザー モード ドライバー フレームワーク (UMDF) 1 ドライバーを移植する方法について説明します。
ms.assetid: 99D20B4C-17C4-42AC-B4D9-F5FD64E10723
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c5a09e25a9d12c4bc7e452b560390d9937560f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551218"
---
# <a name="porting-a-driver-from-umdf-1-to-umdf-2"></a>UMDF 2 に UMDF 1 からドライバーの移植


このトピックでは、UMDF 2 に、ユーザー モード ドライバー フレームワーク (UMDF) 1 ドライバーを移植する方法について説明します。 ソース ディレクトリ/ファイル (Visual Studio プロジェクトされません) を使用する 1 の UMDF ドライバーで開始できます。 または、Visual Studio プロジェクトに含まれている 1 の UMDF ドライバーを変換することができます。 結果は、Visual Studio で 2 の UMDF ドライバーのプロジェクトになります。 2 の UMDF ドライバーは、デスクトップ エディション (Home、Pro、Enterprise、および教育機関向け) の場合は、どちらも Windows 10 および Windows 10 Mobile を実行します。

エコー ドライバーのサンプルでは、UMDF 2 UMDF 1 から移植されたドライバーの例を示します。

-   [Echo サンプル (UMDF バージョン 1)](https://go.microsoft.com/fwlink/p/?LinkId=617707)
-   [Echo サンプル (UMDF バージョン 2)](https://go.microsoft.com/fwlink/p/?LinkId=617708)

## <a name="getting-started"></a>作業の開始


開始するには、Visual Studio で新しいドライバーのプロジェクトを開きます。 選択、 **Visual C++ -&gt;Windows ドライバー -&gt;WDF -&gt;ユーザー モード ドライバー (UMDF 2)** テンプレート。 Visual Studio は、ドライバーを実装する必要があるコールバック関数のスタブを含む部分的に設定されているテンプレートを開きます。 この新しいドライバーのプロジェクトには、2 の UMDF ドライバーの基盤となります。 コードを導入する必要がありますの種類のガイドとして UMDF 2 Echo サンプルを使用します。

次に、既存の 1 の UMDF ドライバー コードを確認し、オブジェクトのマッピングを判断します。 UMDF 1 内の各 COM オブジェクトでは、UMDF 2 に対応する WDF オブジェクトがあります。 たとえば、 **IWDFDevice**インターフェイスが表される WDF デバイス オブジェクトにマップ WDFDEVICE ハンドルでします。 UMDF 1 でのほぼすべてのフレームワークが指定したインターフェイス メソッドでは、UMDF 2 に対応する方法があります。 たとえば、 [ **IWDFDevice::GetDefaultIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff558830)マップ[ **WdfDeviceGetDefaultQueue**](https://msdn.microsoft.com/library/windows/hardware/ff545965)します。

同様に、ドライバーによって提供されるコールバック関数では、2 つのバージョンに対応があります。 第 1 UMDF ドライバーによって提供されるインターフェイスの名前付け規則 (以外の**IDriverEntry**) は*は*オブジェクト*コールバック*Xxx<strong>UMDF 2 の名前付け中に、ドライバーによって提供されるルーチンの規則は*Evt*ObjectXxx</strong>します。 たとえば、 [ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)コールバック メソッドには、マップ[ *EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693)します。

ドライバーでは、UMDF 1 と 2 の両方でコールバック関数が実装されていますが、ドライバーがそのコールバックへのポインターを提供する方法は異なります。 UMDF 1 では、ドライバーはドライバーによって提供されるインターフェイスのメンバーとしてコールバック メソッドを実装します。 ドライバーは、呼び出すことによって、framework のオブジェクトのなどの作成時に、フレームワークでこれらのインターフェイスを登録[ **IWDFDriver::CreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff558899)します。

UMDF 2 で、ドライバーには構成構造でのドライバーが提供するコールバック関数へのポインターなど[ **WDF\_ドライバー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551300)と[ **WDF\_IO\_キュー\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff552359)します。

## <a name="managing-object-lifetime"></a>オブジェクトの有効期間を管理します。


UMDF 1 を使用するドライバーは、参照オブジェクトを削除する安全なタイミングを決定するためにカウントを実装する必要があります。 フレームワークは、ドライバーの代わりに、オブジェクト参照を追跡しているために、2 の UMDF ドライバーでは、参照をカウントする必要はありません。

UMDF 2 では、各フレームワーク オブジェクトは、既定の親オブジェクトを持ちます。 親オブジェクトが削除されたときに、フレームワークには、関連付けられている子オブジェクトが削除されます。 ときにオブジェクトの作成メソッドを呼び出すには、ドライバーなど[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)、既定の親を受け入れることができます、またはカスタムの親で指定できます、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)構造体。 Framework のオブジェクトとその既定の親オブジェクトの一覧は、次を参照してください。 [Framework オブジェクトの概要](summary-of-framework-objects.md)します。

## <a name="driver-initialization"></a>ドライバーの初期化


1 の UMDF ドライバーでは実装、 [ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)インターフェイス。 その[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)コールバック メソッド、ドライバー通常。

-   作成し、デバイスのコールバック オブジェクトのインスタンスを初期化します。
-   呼び出して新しい framework デバイス オブジェクトを作成します。 [ **IWDFDriver::CreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff558899)します。
-   デバイスのキューとその対応するコールバック オブジェクトを設定します。
-   呼び出してデバイスのインターフェイス クラスのインスタンスを作成します。 [ **IWDFDevice::CreateDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff557016)します。

2 の UMDF ドライバーでは実装[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)と[ *EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693)します。 その**DriverEntry**日常的な 2 の UMDF ドライバーを呼び出す通常[ **WDF\_ドライバー\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff551302)初期化するために、ドライバーの[ **WDF\_ドライバー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551300)構造体。 この構造体を渡します[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)します。

その[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)関数の場合、ドライバーには、次のいくつか実行可能性があります。

-   入力、 [WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体は、デバイス オブジェクトを作成するために使用する情報を提供します。 WDFDEVICE の使用の詳細については\_INIT を参照してください[Framework デバイス オブジェクトを作成する](creating-a-framework-device-object.md)します。
-   デバイス オブジェクトの領域のコンテキストを設定します。 割り当てとフレームワーク オブジェクト コンテキストの領域にアクセスする方法については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](framework-object-context-space.md)します。
-   [デバイス オブジェクトを作成](creating-a-framework-device-object.md)です。
-   指定[要求ハンドラー](request-handlers.md)デバイス オブジェクト。
-   [I/O キューを作成する](creating-i-o-queues.md)します。
-   [デバイスのインターフェイスを作成](using-device-interfaces.md)です。
-   設定[アイドル状態のデバイス ポリシー](supporting-idle-power-down.md)と[wake 設定](supporting-system-wake-up.md)デバイス オブジェクトには、電源ポリシーが所有している場合、します。
-   [割り込みオブジェクトを作成する](creating-an-interrupt-object.md)ハードウェア割り込みをサポートしている場合、します。

## <a name="installing-your-driver"></a>ドライバーをインストールします。


Visual Studio で新しいドライバーのプロジェクトを作成すると、新しいプロジェクトには、.inx ファイルが含まれています。 ドライバーをビルドすると、Visual Studio は、ドライバー パッケージの一部として使用できる INF ファイルに、.inx ファイルをコンパイルします。

1 の UMDF ドライバーに対して、INF ファイルには、ドライバーのクラス ID を含める必要があります、中に、DriverCLSID は 2 の UMDF ドライバーの INF ファイルでは必要ありません。

また、1 の UMDF ドライバーの INF ファイルで共同インストーラーを参照する必要があります、constaller 参照は必要ありません UMDF 2 INF ファイル。 共同インストーラーの参照を 2 の UMDF ドライバーの INF ファイルに表示されることが 1 つは必要ありません。

## <a name="storing-device-context"></a>デバイス コンテキストを格納します。


UMDF 1 で、ドライバー通常格納、ドライバーが作成したコールバック オブジェクト内のデバイス コンテキストなど、デバイス コールバック オブジェクトのクラスのプライベート メンバーを指定することでします。 また、1 の UMDF ドライバーを呼び出すことができます、 [ **IWDFObject::AssignContext** ](https://msdn.microsoft.com/library/windows/hardware/ff560208)フレームワーク オブジェクト コンテキストを登録します。

UMDF 2 では、フレームワークはに基づいて省略可能なコンテキストの領域を割り当てます[ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)オブジェクトの作成を呼び出すときに、ドライバーが提供する構造体。メソッド。 オブジェクトを呼び出すと、メソッドの作成、ドライバーを呼び出すことが[ **WdfObjectAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff548723)特定のオブジェクトに追加のコンテキストの領域を割り当てるための 1 つまたは複数の時間。 コンテキストの構造およびアクセサー メソッドを定義する、手順 2.、UMDF ドライバーを使用する必要がありますを参照してください。[フレームワーク オブジェクト コンテキストの空間](framework-object-context-space.md)します。

## <a name="debugging-your-driver"></a>ドライバーのデバッグ


2 の UMDF ドライバーをデバッグするには、Wudfext.dll ではなく Wdfkd.dll で拡張機能を使用します。 Wudfext.dll 拡張機能に関する詳細については、次を参照してください。 [Wdfkd.dll でデバッガー拡張の概要](debugger-extensions-for-kmdf-drivers.md)します。

UMDF 2 で取得することも追加のドライバーがデバッグ情報を転送トレース レコーダー (), 違います」の説明に従って[KMDF および UMDF 2 ドライバーで Inflight トレースの記録機能を使用して](using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)します。 フレームワークの独自の使用も、*インフライト レコーダー* (IFR)。 参照してください[フレームワークのイベントのロガーを使用して](using-the-framework-s-event-logger.md)します。

## <a name="related-topics"></a>関連トピック


[UMDF の概要](getting-started-with-umdf-version-2.md)

[フレームワーク オブジェクト コンテキストの領域](framework-object-context-space.md)

[UMDF バージョン履歴](umdf-version-history.md)

[Framework のオブジェクト](framework-objects.md)

 

 






