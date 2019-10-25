---
title: Oplock の付与
description: Oplock の付与
ms.assetid: 7faf17ef-1596-4952-9575-616f66b37ed6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2886050fe69afa1d9b986e6bb8b6050ea7628d0e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841225"
---
# <a name="granting-oplocks"></a>Oplock の付与


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


Oplock は[FSCTL](https://go.microsoft.com/fwlink/p/?linkid=124238)s によって要求されます。 次の一覧に、さまざまな oplock の種類の FSCTLs を示します (ユーザーモードのアプリケーションとカーネルモードドライバーによって発行される可能性があります)。

-   FSCTL\_要求\_OPLOCK\_レベル\_1

-   FSCTL\_要求\_OPLOCK\_レベル\_2

-   FSCTL\_要求\_バッチ\_OPLOCK

-   FSCTL\_要求\_フィルター\_OPLOCK

-   FSCTL\_要求\_OPLOCK

リスト内の最初の4つの FSCTLs は、レガシ oplock を要求するために使用されます。 最後の FSCTL は、要求に対して Windows 7 の oplock を要求するために使用され\_OPLOCK\_、要求の**Flags**メンバーに指定されている入力\_フラグ\_要求フラグ要求の\_の入力\_バッファー構造[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)の*lpinbuffer*パラメーターとして渡された。\_ 同様の方法で、 [**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を使用して、カーネルモードから Windows 7 の oplock を要求できます。 ファイルシステムミニフィルターでは、 [**FltAllocateCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecallbackdata)と[**FltPerformAsynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltperformasynchronousio)を使用して Windows 7 oplock を要求する必要があります。 4つの Windows 7 oplock が必要であることを指定するために、1つまたは複数のフラグ OPLOCK\_レベル\_キャッシュ\_読み取り、OPLOCK\_レベル\_キャッシュ\_ハンドル、または\_レベル\_キャッシュ\_WRITE は、要求の**RequestedOplockLevel**メンバーに設定されています。\_OPLOCK\_入力\_バッファー構造体です。 詳細については、「 [**FSCTL\_REQUEST\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock)」を参照してください。

Oplock に対する要求が行われ、oplock が許可されると、ファイルシステムは状態\_PENDING を返します (このため、oplock は同期 i/o には許可されません)。 FSCTL IRP は、oplock が解除されるまで完了しません。 Oplock を許可できない場合は、適切なエラーコードが返されます。 最も一般的に返されるエラーコードは、ステータス\_OPLOCK\_\_無効な\_パラメーター (およびそれと同等のユーザーモードのと似)\_状態です。

前述のように、フィルター oplock を使用すると、他のアプリケーション/クライアントが同じストリームにアクセスしようとしたときに、アプリケーションが "バックアウト" できます。 このメカニズムにより、アプリケーションは、ストリームを開こうとしたときに、ストリームの他のアクセサーが共有違反を受信しなくても、ストリームにアクセスできます。 共有違反を回避するには、特別な3段階の手順を使用してフィルター oplock を要求します (FSCTL\_REQUEST\_フィルター\_OPLOCK)。

1.  ファイルに必要なアクセス\_権を使用してファイルを開き\_属性を読み取り、ファイルの共有モード\_共有\_読み取り |ファイル\_共有\_書き込み |ファイル\_共有\_削除します。

2.  手順 1. のハンドルに対してフィルター oplock を要求します。

3.  読み取りアクセス用にもう一度ファイルを開きます。

手順 1. で開かれたハンドルは、他のアプリケーションが共有の違反を受け取ることはありません。これは、データアクセス (ファイル\_読み取り\_データ) ではなく、属性アクセス (ファイル\_読み取り\_属性) に対してのみ開かれているためです。 このハンドルは、フィルター oplock の要求に適していますが、データストリームでの実際の i/o の実行には適していません。 手順 3. で開かれたハンドルを使用すると、oplock の所有者は、ストリームで i/o を実行できます。手順 2. で許可されている oplock を使用すると、oplock の所有者は、ストリームへのアクセスを試みる別のアプリケーションへの共有違反を回避できます。

NTFS ファイルシステムでは、ファイル\_予約\_OPFILTER 作成オプションフラグを使用して、この手順の最適化を行います。 前の手順の手順 1. でこのフラグが指定されている場合は、ファイルシステムが手順2に失敗したと判断した場合に、ファイルシステムによってステータス\_OPLOCK\_\_失敗します。 手順 1. が成功した場合、create 要求に対してファイル\_予約\_OPFILTER が指定されていても、手順2が成功するという保証はありません。

次の表は、oplock を与えるために必要な条件を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[要求の種類]</th>
<th align="left">条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>レベル1</p>
<p>filter</p>
<p>Batch</p></td>
<td align="left"><p>次のすべての条件に該当する場合にのみ許可されます。</p>
<ul>
<li>要求は、ファイルの指定されたストリームを対象としています。
<ul>
<li>ディレクトリの場合は、STATUS_INVALID_PARAMETER が返されます。</li>
</ul></li>
<li>ストリームは非同期アクセス用に開かれています。
<ul>
<li>同期アクセスのために開いた場合、STATUS_OPLOCK_NOT_GRANTED が返されます (同期 i/o 要求に対して oplock は付与されません)。</li>
</ul></li>
<li>ファイルのストリームには<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-kernel-mode-kernel-transaction-manager" data-raw-source="[TxF](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-kernel-mode-kernel-transaction-manager)">TxF</a>トランザクションがありません。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ストリームには他に開いているものはありません (同じスレッドでも)。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
</ul>
<p>現在の oplock 状態がである場合は、次の点に注意してください。</p>
<ul>
<li><p>No Oplock: 要求が許可されます。</p></li>
<li><p>レベル 2: 元のレベル2の要求が FILE_OPLOCK_BROKEN_TO_NONE で破損しています。 要求された排他 oplock が付与されます。</p></li>
<li><p>レベル1、バッチ、フィルター、読み取り、読み取りハンドル、読み取り/書き込み、または読み取り/書き込みハンドル: STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>Level 2</p></td>
<td align="left"><p>次のすべての条件に該当する場合にのみ許可されます。</p>
<ul>
<li>要求は、ファイルの指定されたストリームを対象としています。
<ul>
<li>ディレクトリの場合は、STATUS_INVALID_PARAMETER が返されます。</li>
</ul></li>
<li>ストリームは非同期アクセス用に開かれています。
<ul>
<li>同期アクセスのために開いた場合、STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ファイルに TxF トランザクションがありません。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ストリームに現在のバイト範囲ロックがありません。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
<li>Windows 7 より前のオペレーティングシステムでは、バイト範囲ロックが最後に開かれてからストリームに存在していたかどうかが確認され、要求が失敗した場合はエラーが発生します。</li>
</ul></li>
</ul>
<p>現在の oplock 状態がである場合は、次の点に注意してください。</p>
<ul>
<li><p>No Oplock: 要求が許可されます。</p></li>
<li>レベル2または読み取り: 要求が付与されます。 同じストリームに対して複数のレベル 2/読み取り oplock を同時に許可することができます。 同じハンドルに複数のレベル 2 (読み取り不可) oplock を存在させることもできます。
<ul>
<li>読み取り oplock が既に許可されているハンドルで読み取り oplock が要求された場合、2番目の読み取り oplock が付与される前に、STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE で最初の読み取り oplock の IRP が完了します。</li>
</ul></li>
<li><p>レベル1、バッチ、フィルター、読み取りハンドル、読み取り/書き込み、読み取り/書き込みハンドル: STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>読み取り</p></td>
<td align="left"><p>次のすべての条件に該当する場合にのみ許可されます。</p>
<ul>
<li>要求は、ファイルの指定されたストリームを対象としています。
<ul>
<li>ディレクトリの場合は、STATUS_INVALID_PARAMETER が返されます。</li>
</ul></li>
<li>ストリームは非同期アクセス用に開かれています。
<ul>
<li>同期アクセスのために開いた場合、STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ファイルに TxF トランザクションがありません。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ストリームに現在のバイト範囲ロックがありません。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
</ul>
<p>現在の oplock 状態がである場合は、次の点に注意してください。</p>
<ul>
<li><p>No Oplock: 要求が許可されます。</p></li>
<li>レベル2または読み取り: 要求が付与されます。 同じストリームに対して複数のレベル 2/読み取り oplock を同時に許可することができます。
<ul>
<li>また、既存の oplock に新しい要求と同じ oplock キーがある場合、その IRP は STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE を使用して完了します。</li>
</ul></li>
<li>読み取りハンドルおよび既存の oplock には、新しい要求とは異なる oplock キーがあります。要求が許可されます。 複数の読み取りと読み取りハンドルの oplock を同じストリームに共存させることができます (この表の後の注を参照してください)。
<ul>
<li>それ以外 (oplock キーは同じ) STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li><p>レベル1、バッチ、フィルター、読み取り/書き込み、読み取り/書き込みハンドル: STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>読み取りハンドル</p></td>
<td align="left"><p>次のすべての条件に該当する場合にのみ許可されます。</p>
<ul>
<li>要求は、ファイルの指定されたストリームを対象としています。
<ul>
<li>ディレクトリの場合は、STATUS_INVALID_PARAMETER が返されます。</li>
</ul></li>
<li>ストリームは非同期アクセス用に開かれています。
<ul>
<li>同期アクセスのために開いた場合、STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ファイルに TxF トランザクションがありません。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ストリームに現在のバイト範囲ロックがありません。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
</ul>
<p>現在の oplock 状態がである場合は、次の点に注意してください。</p>
<ul>
<li><p>No Oplock: 要求が許可されます。</p></li>
<li>Read: 要求が付与されます。
<ul>
<li>既存の読み取り oplock に新しい要求と同じ oplock キーがある場合、その IRP は STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE を使用して完了します。 これは、oplock が Read から Read Handle にアップグレードされることを意味します。</li>
<li>新しい要求と同じ oplock キーを持たない既存の読み取り oplock は、変更されずに残ります。</li>
</ul></li>
<li><p>レベル2、レベル1、バッチ、フィルター、読み取り/書き込み、読み取り/書き込みハンドル: STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>読み取り/書き込み</p></td>
<td align="left"><p>次のすべての条件に該当する場合にのみ許可されます。</p>
<ul>
<li>要求は、ファイルの指定されたストリームを対象としています。
<ul>
<li>ディレクトリの場合は、STATUS_INVALID_PARAMETER が返されます。</li>
</ul></li>
<li>ストリームは非同期アクセス用に開かれています。
<ul>
<li>同期アクセスのために開いた場合、STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ファイルに TxF トランザクションがありません。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>(同じスレッドでも) ストリームに他のオープンがある場合は、同じ oplock キーを持つ必要があります。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
</ul>
<p>現在の oplock 状態がである場合は、次の点に注意してください。</p>
<ul>
<li><p>No Oplock: 要求が許可されます。</p></li>
<li>読み取りまたは読み取り/書き込み、既存の oplock には、要求と同じ oplock キーがあります。既存の oplock の IRP は STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE で完了し、要求は許可されます。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li><p>レベル2、レベル1、バッチ、フィルター、読み取りハンドル、読み取り/書き込みハンドル: STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>読み取り/書き込み-ハンドル</p></td>
<td align="left"><p>次のすべてに該当する場合にのみ許可されます。</p>
<ul>
<li>要求は、ファイルの指定されたストリームを対象としています。
<ul>
<li>ディレクトリの場合は、STATUS_INVALID_PARAMETER が返されます。</li>
</ul></li>
<li>ストリームは非同期アクセス用に開かれています。
<ul>
<li>同期アクセスのために開いた場合、STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ファイルに TxF トランザクションがありません。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>(同じスレッドでも) ストリームに他のオープン要求がある場合は、同じ oplock キーを持つ必要があります。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
</ul>
<p>現在の oplock 状態がである場合は、次の点に注意してください。</p>
<ul>
<li><p>No Oplock: 要求が許可されます。</p></li>
<li>読み取り、読み取りハンドル、読み取り/書き込み、または読み取り/書き込みハンドル。既存の oplock には、要求と同じ oplock キーがあります。既存の oplock の IRP は STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE で完了し、要求は許可されます。
<ul>
<li>Else STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li><p>レベル2、レベル1、バッチ、フィルター: STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**注**   読み取りとレベル2の oplock を同じストリームに共存させることができ、読み取りと読み取りハンドルの oplock を共存させることはできますが、レベル2と読み取りハンドルの oplock は共存できない可能性があります。

 

 

 




