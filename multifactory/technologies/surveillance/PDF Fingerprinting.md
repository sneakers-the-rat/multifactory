Found in [[Elsevier]]'s PDFs, alongside [[NISO-RP-8-2008]] [[JAV]] tags, [[ALI]] and [[DOI]]s, in order to identify the downloader of pirated PDFs that end up on [[Sci-Hub]]

A sample:

```json
[
"FCi27mtaKod38ztmGndn-y8NNz.r.lt6SndqGztz_ztr-ngqQm9aMo9eOnMeJntuNntu",
"D2ei2mgqJz9b-m.mGmPqRyLNNnwmOlt7.ywiGmt-Kndr9otqRywv8o9ePmtiNmd2Sn92Tma",
"6U7vcmPuOn9uLnMaGyM7-nLNNntv9lt6RmtaGmweOyMmJnMmSmgmOo9eOnM6LnMaRmM-Tma",
"lXLf8owyQztiMzwqGnMz7zcNNotb7lwf.m9qGzt6Km.qMngqLndqLo9eOotaNm96Mmt6Tma",
"FCi27y9qOnd-Ny96GmPmOmcNNzwf-lwj-m9mGztz7ytaMnM78n9v-o9ePmM6Rm9-Qn9eTma",
"XlEDumMz7nM7-m9iGogmRmLNNyt_8lwiKz9eGm9-Pm.v7ztiLztz_o9eOnMeQnd-Sodm",
"lXLf8yt-JywmNmPeGm9n9n8NNzgn.lt_8zwqGogz7zgn7zt6SyPr-o9eOnM6Pot2Mn9qTma",
"FCi27zgf8mdqMmMeGnMmMy8NNz9eQlweNy.eGmMiMm96Qmgr9nMb-o9ePmtuRmt6JotmTma",
"FCi27nwmKnMeSodeGm.z.y8NNntz.lt-PywmGy9__ngqQmtiPmtb7o9ePmteJotyJoduTma",
"HIoniz.qOnd-Nmt-GmteNn8NNot7.lt-QndaGnPv.mdaMmt6RnMqMo9ePmdmOmdiKod-Tma",
"ZtV1wntuPyPn9z.qGyPv7msNNytz7lwiKyM6GntmJnt_-nteRm.mRo9eOnM6Pot2MnMyTma",
"d2UUdywiJmtz7zt-Gm9eQmcNNzt2Qlwf7m9uGzd_7zdf7owr9yMqOo9ePmtaKnM2NmduTma",
"tprDsnMeJn9iOnweGnPuQnsNNz.eMlt-Qm.mGotz.ytiNz.yRmd-Mo9eOnM6Pot2OmM6Tma",
"tprDsyPiNn9iQn9-GmMiSy8NNn96Llwf9owiGowqQyMiRzwv_ngqPo9eOnM6Pot2OndyTma",
"ZIFNOztmRotn9owiGzduNmsNNnd-Rlt_8otiGot-Oy92QnMeSyMqKo9eOnM6Pot2OntaTma",
"D2ei2nMb_zwmSowyGzwv8mLNNotj8lt-My9yGmtaModaNm92RytySo9ePmtaKn92Qmt2Tma",
"d2UUdot__owr-y9mGodqLocNNn.eOlwmPmtaGmgj7ndn_nMiMndiNo9ePmdiLnMmPotmTmq",
"6U7vcmtuSndmSntqGmdiMy8NNnPz7lt_7ndeGmtv7n9eLndj_zduJo9ePmtiOntmNntmTma",
"ZtV1wn9mMnd2MzwiGz9eRysNNmgySlt7_ot-Gy97.mgiKotqKnt_.o9eOnM6Pot2Mn96Tma",
"XlEDuyweNmtz9ntqGm9aMocNNodr9lt__z9iGmdj_n9yNnt6Sm9-Lo9ePmd6KotmRnM2Tma",
"HIonintn-z9uPogmGnMeSzsNNogf-lwj.z.qGmgqSn9yPndf7mdmLo9eOotuLm9aNodqTma",
"ZlkjsyMj7mPr.ndiGowuMmcNNy.mNlwj9m.yGmtb7z.qRz.iKyt38o9eOnM6Pot2MnMeTma",
"Dpairmdj9mPr8nwmGn.r7z8NNnMb7lwj8otiGyt-MzwuKzd__nt39o9ePmtaPotaJm9-Tma",
"6mIUqngiNzduNn9iGmgeJnsNNot2Rlt-SzguGzt2Oodf_n.eNodz.o9eOn9mQnMqOm9e",
"FCi27mwr_mPn-m.mGmPuKncNNmduOlweOytuGogj.yMv-z92Pyt6Mo9eOnM6Pot2Mn9yTma",
"6U7vcngj-zt2Ln.uGodr8mcNNmdeSlweKmd2Gzdz9nM3_mgf7yt2Ro9ePmt6Sn9qLntyTma",
"zjJBNmPn.mdiRntiGzgmPnLNNmM2Klt6JmMqGy9aNz9aMmdv_mwuNo9ePm96Qm9iRndiTma",
"FCi27mPmRnPiKngeGngqJzcNNogj8lwj-zwiGnPiLmtb7y9qKzgeMo9eOnMeLn9aNm9m"
]

```

## Mitigating

Use exiftool and qpdf

A [Bash Script](https://gist.github.com/sneakers-the-rat/172e8679b824a3871decd262ed3f59c6)

```bash
# Color Codes so that warnings/errors stick out
GREEN="\e[32m"
RED="\e[31m"
CLEAR="\e[0m"

# loop through all PDFs in first argument ($1),
# or use '.' (this directory) if not given
DIR="${1:-.}"

echo "Cleaning PDFs in directory $DIR"

# use find to locate files, pip to while read to get the
# whole line instead of space delimited
# Note -- this will find pdfs recursively!!
find $DIR -type f -name "*.pdf" | while read -r i
do
  
  # output file as original filename with suffix _clean.pdf
  TMP=${i%.*}_clean.pdf

  # remove the temporary file if it already exists
  if [ -f "$TMP" ]; then
      rm "$TMP";
  fi

  exiftool -q -q -all:all= "$i" -o "$TMP"
  qpdf --linearize --replace-input "$TMP"
  echo -e $(printf "${GREEN}Processed ${RED}${i} ${CLEAR}as ${GREEN}${TMP}${CLEAR}")

done
```


## Extracting

### Regex
* Python: `'<([0-9A-Za-z_.-]{40,})/>'`
* grep: `grep -Ena '<[^/]{50,}/>' *.pdf` - https://gist.github.com/sneakers-the-rat/6d158eb4c8836880cf03191cb5419c8f?permalink_comment_id=4043703#gistcomment-4043703
* grep: `grep -Ea '<[a-zA-Z0-9._\-]{50,}?\/>' **/*.pdf` - https://twitter.com/Jofkos/status/1486244612960366593?s=20&t=UHSTwZAWd2okE8kW5A5CWg
* sed: `sed -n '/<?xpacket begin/,/<?xpacket end/s/.*<\([0-9A-Za-z_.-]\{60,\}\)\/>.*/\1/p;t'` - https://twitter.com/horsemankukka/status/1486660383800713216?s=20&t=UHSTwZAWd2okE8kW5A5CWg

### Python Example

```python
import exiftool
from pathlib import Path
import json
import pdb
import re

paper_root = Path().home() / 'location/of/papers'

hashes = []
get_n = 100

processed = 0

rehash = re.compile(r'<([0-9A-Za-z_.-]{40,})/>')

try:
    with exiftool.ExifTool() as et:
        for path in paper_root.glob('**/*.pdf'):
            md = et.execute(b'-b', b'-xmp', str(path).encode('utf-8'))
            try:
                md = md.decode('utf-8')
            except UnicodeDecodeError:
                print(f'Couldnt decode {path}')
                continue
            ahash = rehash.findall(md)
            hashes.extend(ahash)
            if len(ahash)>0:
                processed += 1

finally:

    with open('elsev_hashes.json', 'w') as hashfile:
        json.dump(hashes, hashfile, indent=2)

print(f'processed {processed} files')
```