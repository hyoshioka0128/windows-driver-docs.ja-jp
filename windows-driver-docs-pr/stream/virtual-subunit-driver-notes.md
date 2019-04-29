---
title: 仮想サブユニット ドライバーに関する注意事項
description: 仮想サブユニット ドライバーに関する注意事項
ms.assetid: e484f815-73a8-46f1-956e-ee16b1856bd0
keywords:
- Avc.sys 関数ドライバー WDK、仮想のサブユニット ドライバー
- 仮想のサブユニット ドライバー WDK AV/C
- 外部デバイス WDK AV/C
- IOCTL_AVC_CLASS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdc3a6571c1b9e1dd97f32dd6b707ded0ec3bfad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329958"
---
# <a name="virtual-subunit-driver-notes"></a>仮想サブユニット ドライバーに関する注意事項


仮想のサブユニット ドライバー要求に応答コントロール、状態、および通知 AV/C コマンド外部の AV/C デバイスからを使用して、 [ **IOCTL\_AVC\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560789)インターフェイスを*Avc.sys*します。

IOCTL\_AVC\_クラスのサブ機能はコード[ **AVC\_関数\_取得\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff554163)と[ **AVC\_関数\_送信\_応答**](https://msdn.microsoft.com/library/windows/hardware/ff554170)は仮想サブユニット ドライバーが仮想ドライバー スタックの残りの部分と対話する主要機構です。 仮想のサブユニット ドライバーの送信、 **AVC\_関数\_取得\_要求**IRP を*Avc.sys*でその[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)ルーチン (IRP 後\_MN\_開始\_デバイスが、基になるドライバー スタック内で完了)。 I/O 完了ルーチン、 **AVC\_関数\_取得\_要求**IRP が呼び出される仮想サブユニットの要求を受信します。 I/O 完了ルーチンは、応答を送信する必要があります (によって**AVC\_関数\_送信\_応答**非同期の IRP で)、を使用(AV/Cプロトコル規則に従って);100ミリ秒以内で[ **AVC\_コマンド\_IRB** ](https://msdn.microsoft.com/library/windows/hardware/ff554140)応答を送信する要求に含まれている構造体。 それを再送信する必要があり、 **AVC\_関数\_取得\_要求**IRP が最後に、応答の I/O 完了ルーチンから戻る前に。

仮想ドライバー スタックのサブユニット ドライバーは、外部のデバイスに直接コマンドを送信することはできません。 ピアのドライバー スタックは、この機能を提供します。 ただし、仮想のサブユニット ドライバーを使用できる、 [ **AVC\_関数\_検索\_ピア\_は**](https://msdn.microsoft.com/library/windows/hardware/ff554152)と[ **AVC\_関数\_ピア\_は\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff554168)の subfunctions [ **IOCTL\_AVC\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560789)を検出し、参照のインスタンスをピア*Avc.sys*し、外部の AV/C サブユニットと対話します。

列挙するには、各仮想サブユニットの*Avc.sys*対応するデバイス オブジェクトを作成します。 そのため、仮想のサブユニットが追加され、削除、 *Avc.sys*バスのリセットの IEEE 1394 をトリガーします。 このリセットは、コンピューターに公開される新しい機能を検出するために IEEE 1394 バス上の他のデバイスを許可します。 仮想のサブユニット ドライバーをロードしてに基づいて、 *Avc.sys*インスタンスのレジストリ設定と追加および IOCTL コード要求によって実行時に削除できます。 なお*Avc.sys*ロードを追加して、これらのサブユニットを削除、および最高のサブユニット識別子を持つ対応する仮想サブユニット ドライバーをアンロードするように、同じ種類の複数の仮想サブユニット区別できません。

仮想のサブユニット ドライバーは、シックかシンかにできます。 唯一の要件は、WDM ドライバーとして記述することができます。 シック ドライバーは、最も、すべてではないにも、仮想デバイスの機能を実装します。 シン ドライバーでは、別のドライバーまたはユーザー モード コンポーネント、仮想デバイスの機能に、プロキシ インターフェイスを提供します。 ユーザー モードと仮想のサブユニット ドライバー間のインターフェイスは実装固有であり、デバイスのプライベート インターフェイスの IOCTL コードから実行できます (を参照してください[ **IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506))、または[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139) (WMI)。

VEN\_と MOD\_の仮想インスタンスを原因となった INF ファイルで指定したのと同じ値では*61883.sys*を読み込めません。 TYP\_と ID\_ときに指定された値は*Avc.sys*仮想のサブユニットを列挙します。

仮想のサブユニットの列挙体を使用して行われます、 [ **IOCTL\_AVC\_UPDATE\_仮想\_サブユニット\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560798)、 [ **IOCTL\_AVC\_削除\_仮想\_サブユニット\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560793)、および[ **IOCTL\_AVC\_BUS\_リセット**](https://msdn.microsoft.com/library/windows/hardware/ff560783) IOCTL コード。

適切なの IEEE 1394 Ioctl を送信する必要がある**IEEE1394\_API\_追加\_仮想\_デバイス**と**IEEE1394\_API\_削除\_仮想\_デバイス**列挙プロセスを開始します。 詳細については (IOCTL のサブコマンド\_IEEE1394\_API\_要求)。 *61883.inf*ファイルには、この目的のデバイス識別子 (ID) 既にが含まれています。V1394\\A02D & 10001 が、カスタムの INF ファイルを別の識別子を指定する場合があります。

静的に仮想のサブユニットを列挙する別の方法は、INF ファイルを使用して実現できます。

仮想デバイスの一覧キー下の各値は、パックされたサブユニット アドレス (サブユニット型と最大識別子組み合わせると、AV/C 全般の仕様」の説明に従って) です。 サブユニット アドレスに関連付けられている名前が関係ありませんが、そのインスタンスの一意である必要があります。 プログラムで作成されると、値の名前には、競合を回避するために連続する番号が与えられます。

たとえば、INF ファイルで 1 つの仮想チューナーのサブユニットを作成するには次を使用して**AddReg**ディレクティブ。

```INF
[Subunit_Device.NT.HW.AddReg]
HKR,%VirtualAvc.DeviceList%,Tuner,0x00000001,0x28 ;0x00000001 = Binary value, 0x28 = Registry key value
```

このディレクティブが追加、REG\_0x28 のバイナリ値 (最下位の 3 つのビットにまとめられて、最上位 5 つのビットと 0x0 の識別子の最大のサブユニット型 0x5 がまとめられます)。 ここで「0x0」最大の識別子では、その型の 1 つサブユニットあるを意味します。

**注**  :定義する必要も、`%VirtualAvc.DeviceList%`トークンで、`[Strings]`サブユニットの INF ファイルのセクション。
