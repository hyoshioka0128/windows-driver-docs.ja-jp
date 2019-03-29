---
title: UMDF ドライバーでのバッファー アクセス方法の管理
description: UMDF ドライバーを作成する場合に、フレームワークを使用するバッファーのアクセス方法の基本設定の読み書きデバイス I/O 制御要求と同様に、要求を指定できます。
ms.assetid: BDB78BCD-1964-431B-BE99-CABA6DF44D7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4565b87f69d248af8b8944a0acf08461e9d94e50
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580982"
---
# <a name="managing-buffer-access-methods-in-umdf-drivers"></a>UMDF ドライバーでのバッファー アクセス方法の管理


指定できます UMDF ドライバーを記述するかどうか、*設定*の[アクセス メソッドをバッファー](https://msdn.microsoft.com/library/windows/hardware/ff540701)読み取ったり書き込んだり、要求とデバイスの I/O 制御要求に、フレームワークを使用します。 UMDF ドライバーを提供する値のみの設定は、フレームワークによって使用されるとは限りません。

-   [優先バッファーへのアクセス方法を指定します。](#specifying-preferred-buffer-access-method)
-   [I/O 要求のアクセス方法を取得します。](#retrieving-access-method)
-   [I/O もダイレクト I/O バッファーからは、どちらの変換](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)

## <a href="" id="specifying-preferred-buffer-access-method"></a>優先バッファーへのアクセス方法を指定します。


UMDF バージョン 2.0 以降、UMDF ドライバーを呼び出す[ **WdfDeviceInitSetIoTypeEx** ](https://msdn.microsoft.com/library/windows/hardware/dn265604)を読み取り/書き込み要求の優先アクセス方法を登録し、デバイスの I/O 要求を制御します。

ドライバーが要求されていない場合[ **WdfDeviceInitSetIoTypeEx**](https://msdn.microsoft.com/library/windows/hardware/dn265604)UMDF がこのデバイスへの I/O 要求のバッファー内のメソッドを使用します。

フレームワークは、次の規則を使用して判断するために使用するメソッドへのアクセスします。

-   ドライバー スタックのすべての UMDF ドライバーは、デバイスのバッファーにアクセスするため、同じメソッドを使用する必要があり、フレームワークにより、バッファー内の I/O を優先します。

    UMDF では、他のドライバーの使用のみバッファー I/O デバイスの中に、一部のドライバーでバッファー内の I/O またはデバイスのダイレクト I/O のいずれかを好むことを決定、UMDF はすべてのドライバー バッファー内の I/O を使用します。 1 つ以上のスタックのドライバーは、ダイレクト I/O だけを好む開発者も、バッファー内の I/O だけを必要に応じて、UMDF は、システム イベント ログにイベントが記録し、ドライバー スタックを開始できません。

    ドライバーが呼び出せる[ **WdfDeviceGetDeviceStackIoType** ](https://msdn.microsoft.com/library/windows/hardware/dn265602) UMDF がデバイスの読み取り/書き込みに割り当てられているバッファーへのアクセス方法を決定する要求と I/O 制御要求。

-   場合によっては、UMDF には、デバイスにダイレクト I/O が割り当てられますが、最適なパフォーマンス、使用は、デバイスの要求の 1 つ以上の I/O をバッファーします。 たとえば、UMDF は、ドライバーのバッファーへのデータ コピーに直接アクセスするためのバッファーをマップできるよりも高速、場合、小さなバッファーのバッファー内の I/O を使用します。

    必要に応じて、ドライバーを指定できます、 **DirectTransferThreshold**を呼び出すときに値[ **WdfDeviceInitSetIoTypeEx**](https://msdn.microsoft.com/library/windows/hardware/dn265604)します。 フレームワークでは、この値を使用して、フレームワークがダイレクト I/O を使用する最小バッファー サイズを確認します。 通常、フレームワークは、最適なパフォーマンスを提供する設定を使用するために、この値を指定する必要はありません。

-   UMDF を開始し、メモリ ページの境界で終了するバッファー領域のみのダイレクト I/O を使用します。 先頭またはバッファーの末尾がページの境界上に入らない場合 UMDF はバッファーの部分のバッファー内の I/O を使用します。 つまり、UMDF バッファー内の I/O とダイレクト I/O の両方オプションは使用のいくつかの I/O 要求で構成される大規模なデータ転送。

-   すべてのデバイスの UMDF ドライバーと呼ばれるダイレクト I/O と場合にのみ、I/O 制御コード (IOCTL) が指定されている場合のみデバイス I/O 制御の要求の UMDF がダイレクト I/O を使用[ **WdfDeviceInitSetIoTypeEx** ](https://msdn.microsoft.com/library/windows/hardware/dn265604)直接アクセスする方法を指定します。

## <a href="" id="retrieving-access-method"></a>I/O 要求のアクセス方法を取得します。


ドライバーは、バッファーのアクセス方法に関係なく、データ バッファーへのアクセスに同じ一連の要求オブジェクトのメソッドを使用します。 そのため、ほとんどのドライバー通常必要はないかどうか UMDF はまたはを使用してバッファー内の I/O ダイレクト I/O の I/O 要求を把握します。

場合によっては、I/O 要求のアクセス方法がわかっている場合、ドライバーのパフォーマンスを向上できます。 たとえば、通常ダイレクト I/O を使用する高スループット デバイスがあるとします。 ドライバーは、I/O 要求を受け取る検証用のドライバーをローカル メモリに共有バッファー領域からデータをコピーします。

ただし、ドライバーは、バッファー内の I/O に使用するバッファーを受け取ることがあります。 I/O マネージャーが、中間のバッファーにこのデータをコピーして既に、ため、ドライバーがローカルでのパラメーターをコピーする必要はありません。 コピー操作を避けることで、ドライバーには、パフォーマンスが向上します。

UMDF ドライバーは呼び出し[ **WdfRequestGetEffectiveIoType** ](https://msdn.microsoft.com/library/windows/hardware/dn265616) I/O 要求をバッファーへのアクセス メソッドを取得します。 前述のようデバイスのフレームワークに割り当てられた I/O 型の設定から、特定の要求の I/O の種類が異なる場合があります。

## <a href="" id="using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers"></a> I/O もダイレクト I/O バッファーからは、どちらの変換


UMDF ドライバーでは、「も」メソッドを使用できません。

ただし、[定義](https://msdn.microsoft.com/library/windows/hardware/ff543023)コード (Ioctl) が、要求が「も」メソッドを使用することを指定の一部のデバイスの I/O 制御します。 必要に応じて、UMDF ドライバーは、このようなデバイスの I/O 制御要求のバッファーへのアクセス メソッド I/O バッファーへの変換またはダイレクト I/O。 次の手順を使用します。

1.  含める、 [UmdfMethodNeitherAction](specifying-wdf-directives-in-inf-files.md)ディレクティブで、 [ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)ドライバーの INF ファイル。 ディレクティブの UMDF ドライバーへのアクセス「も」方法を使用するデバイス I/O 制御要求を渡す必要があることを示す値を設定することができます。 (それ以外の場合、UMDF がエラー状態の値を持つこれらの I/O 要求を完了する。)

2.  UMDF には、オブジェクトのメソッドを使用して、I/O 要求のバッファーにアクセス[I/O バッファー](https://msdn.microsoft.com/library/windows/hardware/ff540701#buffered)または[ダイレクト I/O](https://msdn.microsoft.com/library/windows/hardware/ff540701#direct)します。

UMDF がバッファー内の I/O またはダイレクト I/O アクセス メソッドを変換できる場合にのみ、「も」メソッドを使用する IOCTL 要求のサポートを有効にする必要があります。 IOCTL で説明されているバッファーの仕様の規則に従っていないカスタマイズされた要求を指定する場合など、 [I/O 制御コードの説明をバッファー](https://msdn.microsoft.com/library/windows/hardware/ff540663)UMDF にバッファーを変換できません。

 

 





