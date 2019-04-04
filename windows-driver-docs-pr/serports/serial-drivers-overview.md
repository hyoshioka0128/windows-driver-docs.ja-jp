---
title: シリアル コントローラー ドライバーの概要
description: Windows のすべてのバージョンでは、コント ローラーのシリアル デバイス ドライバーのサポートを提供します。
ms.assetid: 1EA0221E-0F68-429B-9DA5-4AE2D3394A09
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df26e9220e3976f482deb9035faf3380b1f45b05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578872"
---
# <a name="serial-controller-drivers-overview"></a>シリアル コントローラー ドライバーの概要


Windows のすべてのバージョンでは、コント ローラーのシリアル デバイス ドライバーのサポートを提供します。 用語*シリアル コント ローラー* 16550 ユニバーサル非同期受信側の送信元 (UART) または互換性のあるデバイスを指します。 シリアルのコント ローラーでは、逐次的に接続されている周辺機器と通信するシリアル ポートを持ちます。 シリアル通信をサポートするために Windows には、以下のようと Serenum.sys ドライバーとシリアル フレームワークの拡張機能 (SerCx および SerCx2) のバージョン 1 および 2 が含まれています。

## <a name="serialsys-and-serenumsys"></a>以下のようと Serenum.sys


Windows 2000 以降では、システムが指定したシリアル ドライバー、際に、サポート、スタンドアロンのシリアル ポート[COM ポート](configuration-of-com-ports.md)とマルチポート ボード。 シリアル列挙型のシステム提供のドライバー、Serenum.sys、スタックまたは互換性のあるシリアル ポート ドライバーによって制御されているシリアル ポートに接続されているデバイスを列挙します。 通常、際に、Windows を実行している PC の場合の上にある COM ポート (COM1、COM2、通常という名前) を制御します。 これらのポートは疎、rs-232 標準に準拠させるが、Pc をサポートするために進化してきました (たとえば、電圧レベル、暗証番号 (pin) の接続、およびハードウェア フロー制御)、事実上の標準をさらに組み込むことです。 詳細については、[際に使用すると Serenum.sys](using-serial-sys-and-serenum-sys.md)を参照してください。

GitHub では、Windows ドライバーのサンプル リポジトリにはソース コードが含まれています、[シリアル](https://go.microsoft.com/fwlink/p/?LinkId=617962)と[Serenum](https://go.microsoft.com/fwlink/p/?LinkId=617961)ドライバーのサンプルと同様に動作し、代わりに、受信トレイの際にインストールすることができますSerenum.sys ドライバー。

## <a name="sercx-and-sercx2"></a>SerCx と SerCx2


Windows 8 以降、SerCx は、integrated 回路基板の間でのシリアル通信をサポートするシステム提供のコンポーネントです。 SerCx は拡張機能、[カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF)。 この拡張機能は、シリアル コント ローラーのカスタムのドライバーの開発を簡略化します。 SerCx シリアル コント ローラーに共通する処理タスクの多くを処理することによって、シリアル コント ローラーの拡張機能ベースのドライバーを支援します。 このドライバーと通信を介して SerCx、 [SerCx デバイス ドライバー インターフェイス](https://msdn.microsoft.com/library/windows/hardware/dn265348)します。

Windows 8.1 以降、SerCx2 によって SerCx が優先されます。 SerCx2 では、多くの機能強化をサイズとコント ローラーのシリアル ドライバーの複雑さを軽減する SerCx にします。 具体的には、SerCx2 とシリアル コント ローラーへのアクセスの競合が発生する I/O トランザクションをコーディネートのタイムアウトの管理に必要な処理作業のシリアル コント ローラーのドライバーを緩和します。 その結果、シリアル コント ローラー ドライバーは、小規模で単純なは。 シリアル コント ローラーのハードウェア ベンダーには、シリアルのコント ローラーのハードウェアに固有の機能を管理する、汎用コント ローラーのシリアル タスクを実行する SerCx2 に依存した拡張機能に基づくシリアル コント ローラー ドライバーが用意されています。 このドライバーと通信を介して SerCx2、 [SerCx2 デバイス ドライバー インターフェイス](https://msdn.microsoft.com/library/windows/hardware/dn265349)します。

SerCx2 の詳細については、[シリアルのフレームワークの拡張機能 (SerCx2) のバージョン 2 を使用して](using-version-2-of-the-serial-framework-extension.md)を参照してください。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="serial-i-o-request-interface.md" data-raw-source="[Serial I/O Request Interface](serial-i-o-request-interface.md)">I/O 要求をシリアル インターフェイス</a></p></td>
<td><p>シリアル コント ローラーで、クライアントのポートに接続されている周辺機器を制御するには、アプリケーションまたは周辺機器のデバイス ドライバーは、ポートに I/O 要求を送信します。</p></td>
</tr>
<tr class="even">
<td><p><a href="differences-between-sercx2-and-serial-sys.md" data-raw-source="[Differences Between SerCx2.sys and Serial.sys](differences-between-sercx2-and-serial-sys.md)">SerCx2.sys とスタックの違い</a></p></td>
<td><p>受信トレイ Sercx2.sys とスタック ドライバー コンポーネントは、両方の実装が、<a href="serial-i-o-request-interface.md" data-raw-source="[serial I/O request interface](serial-i-o-request-interface.md)">シリアルの I/O 要求インターフェイス</a>、これらのコンポーネントに置き換えることはできません。 異なる要件のセットを満たすために、設計されています。</p></td>
</tr>
</tbody>
</table>

 

 

 




