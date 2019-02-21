---
title: WCIFS\_リダイレクト\_ECP\_CONTEXT 構造体
description: 特定の操作を作成するファイルのリダイレクト状態をについて説明します。
ms.assetid: 6101490D-54B9-4A34-ADB5-9CC2B855691D
keywords:
- WCIFS_REDIRECTION_ECP_CONTEXT 構造インストール可能なファイル システム ドライバー
- PWCIFS_REDIRECTION_ECP_CONTEXT 構造体ポインター インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- WCIFS_REDIRECTION_ECP_CONTEXT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0c61818f522849d9738d622feee193944ff2faa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529715"
---
# <a name="wcifsredirectionecpcontext-structure"></a>WCIFS\_リダイレクト\_ECP\_CONTEXT 構造体


特定の操作を作成するファイルのリダイレクト状態をについて説明します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _WCIFS_REDIRECTION_ECP_CONTEXT {
  USHORT      Size;
  USHORT      Flags;
  FILE_ID_128 FileId;
  GUID        VolumeGuid;
} WCIFS_REDIRECTION_ECP_CONTEXT, *PWCIFS_REDIRECTION_ECP_CONTEXT;
```

<a name="members"></a>Members
-------

**サイズ**  
構造体のサイズ`sizeof(WCIFS_REDIRECTION_ECP_CONTEXT)`します。

**フラグ**  
ファイルのリダイレクトの状態を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-layer"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER</strong> 0x0001</td>
<td align="left"><p>これは LayerRootLocations のレジストリ キーに登録されていない層からリダイレクトされたファイルです。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-scratch"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_SCRATCH</strong> 0x0002</td>
<td align="left"><p>これは、新しいまたは変更されたファイルではリダイレクトされません。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-registered-layer"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REGISTERED_LAYER</strong> 0x0004</td>
<td align="left"><p>これは、LayerRootLocations レジストリ キーに記載されているレイヤーからリダイレクトされたファイルです。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-remote-layer"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REMOTE_LAYER</strong> 0x0008</td>
<td align="left"><p>これは、コンテナーを基準としてリモート ファイル システムからリダイレクトされたファイルです。 これは、そのサーバー上のレイヤーとして登録されていない可能性がありますもかまいません。 HYPER-V コンテナーでは、リモート サーバーは、HYPER-V コンテナー ユーティリティ VM のホストです。</p></td>
</tr>
</tbody>
</table>

 

**FileId**  
バックアップ ファイルの識別子。

**VolumeGuid**  
バックアップ ファイルが存在するディスク ボリュームの GUID ベースの識別子です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10 バージョン 1607</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h</td>
</tr>
</tbody>
</table>

 

 





