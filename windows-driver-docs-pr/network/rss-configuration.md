---
title: RSS 構成
description: RSS 構成
ms.assetid: 84a00163-6908-439a-a980-c13f0ec8e3c1
keywords:
- 受信側のスケーリング WDK ネットワーク、ndirection テーブルの例
- RSS WDK ネットワーク, 間接テーブルの例
- 受信側のスケーリング WDK ネットワーク, 構成
- RSS WDK ネットワーク, 構成
- ndirection テーブルの例 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cdfd45a7f93baef9b0f5d933c85340ed8dfea42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842013"
---
# <a name="rss-configuration"></a>RSS 構成





RSS の構成情報を取得するために、1つ前のドライバーが Oid\_GEN の OID クエリを送信し、 [\_スケール\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-capabilities)をミニポートドライバーに\_できます。 また、NDIS は、初期化中に[ **\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造をバインドする\_、ndis のプロトコルドライバーに RSS 構成情報を提供します。

このドライバーは、ハッシュ関数、型、および間接参照テーブルを選択します。 これらの構成オプションを設定するために、ドライバーは Oid\_GEN の OID セット要求を送信し、 [\_\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-parameters)をミニポートドライバーに\_受信します。 それまでのドライバーは、この OID を照会して現在の RSS 設定を取得することもできます。 OID\_GEN\_の情報バッファーには、\_スケール\_パラメーター OID が含まれています。これには、 [**NDIS\_receive\_scale\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)構造体へのポインターが含まれています。

このドライバーは、NIC で RSS を無効にすることができます。 この場合、ndis\_RSS\_PARAM\_フラグが設定されます。このフラグは、NDIS\_RECEIVE\_SCALE\_PARAMETERS 構造体の**Flags**メンバーの\_rss フラグ\_無効にします。 このフラグが設定されている場合、ミニポートドライバーは、他のすべてのフラグと設定を無視し、NIC で RSS を無効にする必要があります。

NDIS は OID\_GEN を処理してから、ミニポートドライバーに渡す前に\_\_パラメーターを受信\_し、必要に応じて、ミニポートアダプターの \*RSS 標準化されたキーワードを更新します。 **\*rss**キーワードの詳細については、「 [Rss 用の標準化](standardized-inf-keywords-for-rss.md)された INF キーワード」を参照してください。

OID\_GEN を受信した後\_\_\_rss\_PARAM\_フラグが設定された[\_スケール\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-parameters)セット要求を受け取ります。\_rss フラグセットを無効にすると、ミニポートドライバーは、初期化後に NIC の RSS 状態を nic の初期状態に設定する必要があります。 したがって、ミニポートドライバーがそれ以降の OID\_\_GEN を受け取る場合は、\_スケール\_パラメーターセット要求を NDIS\_RSS\_\_に設定する必要があります。\_RSS フラグをオフにすると、すべてのパラメーターには、ミニポートアダプターが初期化された後に初めて\_\_を受け取るように設定されます。\_\_\_

後のドライバーでは、 [oid\_GEN\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-hash)使用して\_ハッシュ OID を受け取ることができます。これにより、RSS を有効にしなくても、受信したフレームでハッシュ計算を有効化および構成できます。 また、この OID を照会して現在の受信ハッシュ設定を取得することもできます。

OID\_GEN\_RECEIVE\_HASH OID の情報バッファーには、 [**NDIS\_receive\_hash\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)構造体へのポインターが含まれています。 Set 要求の場合、OID はミニポートアダプターが使用する必要があるハッシュパラメーターを指定します。 クエリ要求の場合、OID はミニポートアダプターが使用しているハッシュパラメーターを返します。 この OID は、RSS をサポートするドライバーでは省略可能です。

**注**  受信ハッシュ計算が有効になっている場合、NDIS は RSS を有効にする前に、受信ハッシュ計算を無効にします。 RSS が有効になっている場合、NDIS は、receive hash の計算を有効にする前に RSS を無効にします。

 

ミニポートドライバーがサポートするすべてのミニポートアダプターは、後続のすべてのプロトコルバインドに同じハッシュ構成設定を提供する必要があります。 この OID には、ミニポートドライバーまたは NIC がハッシュ計算に使用する必要がある秘密キーも含まれています。 キーは320ビット長 (40 バイト) で、それ以降のドライバーが選択する任意のデータ (バイトのランダムストリームなど) を含めることができます。

処理負荷を再調整するために、前のドライバーで RSS パラメーターを設定し、間接テーブルを変更することができます。 通常、間接テーブルを除き、すべてのパラメーターは変更されません。 ただし、RSS が初期化された後、それ以降のドライバーによって他の RSS 初期化パラメーターが変更される可能性があります。 必要に応じて、ミニポートドライバーは NIC ハードウェアをリセットして、ハッシュ関数、ハッシュシークレットキー、ハッシュの種類、基本 CPU 番号、または間接テーブルのインデックス作成に使用されるビット数を変更できます。

これらのパラメーターは、それ以降のドライバーによっていつでも設定でき  ことに**注意**してください。 これにより、順序が不足する可能性があります。 TCP をサポートするミニポートドライバーは、このインスタンスの受信キューを削除する必要はありません。

 

次の図は、間接テーブルの2つのインスタンスのコンテンツの例を示しています。

![rss 間接テーブルの2つのインスタンスの内容を示す図](images/rss-table.png)

上の図は4つのプロセッサ構成を前提としており、ハッシュ値から使用される最下位ビットの数が6ビットであることを前提としています。 このため、間接参照テーブルには64エントリが含まれています。

図の表 A では、初期化の直後に間接テーブルの値が一覧表示されます。 その後、通常のトラフィック負荷が変化すると、プロセッサの負荷が不均衡になります。 このドライバーは、不均衡な状態を検出し、新しい間接テーブルを定義することによって負荷の再調整を試みます。 テーブル B には、新しい間接テーブルの値が一覧表示されます。 表 B では、CPU 2 からの負荷の一部が Cpu 1 と3に移動されています。

**注**  間接テーブルが変更された場合 (現在の受信記述子キューが処理されている間)、パケットが間違った CPU で処理される可能性があります。 これは、通常の一時的な状態です。

 

間接テーブルのサイズは、通常、システムのプロセッサ数の 2 ~ 8 倍です。

ミニポートドライバーがパケットを Cpu に配布するときに Cpu が多すぎると、負荷の分散に費やされた労力が膨大になる可能性があります。 この場合、ドライバーは、ネットワークデータの処理が発生する Cpu のサブセットを選択する必要があります。

場合によっては、使用可能なハードウェア受信キューの数が、システムの Cpu 数よりも少なくなることがあります。 ミニポートドライバーは、間接参照テーブルを調べて、ハードウェアキューに関連付ける CPU 数を確認する必要があります。 間接テーブルに表示される CPU の数が、NIC がサポートするハードウェアキューの数より多い場合、ミニポートドライバーは間接テーブルから CPU 番号のサブセットを選択する必要があります。 サブセットの数は、ハードウェアキューの数と同じです。 ミニポートドライバーは、OID\_GEN から**Indirection Tablesize**パラメーターを取得して、 [\_の\_パラメーターを受け取る\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-parameters)ます。 ミニポートドライバーは、OID\_GEN に応答して**Numberofreceivequeues**値を指定し、\_のスケール\_機能を受信\_ます。

 

 





