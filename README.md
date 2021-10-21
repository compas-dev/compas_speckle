# COMPAS Speckle

This is repo is work-in-progress.
Please feel free to contribute!

---

Data Bridge between COMPAS and Speckle.

[... long description ...]

## Getting Started

```bash
conda create -n speckle-test compas
conda activate speckle-test
pip install specklepy
```

## Basic Example

```python
from compas.data import DataDecoder
from compas.data import DataEncoder

from specklepy.objects import Base


class SpeckleDataBridge(Base):
   data: dict = {}

   @classmethod
   def from_compas(cls, compas_obj):
       encoder = DataEncoder()
       return cls(data=encoder.default(compas_obj))

   def to_compas(self):
       decoder = DataDecoder()
       return decoder.object_hook(self.data)


if __name__ == '__main__':

    from compas.datastructures import Mesh
s
    from specklepy.api import operations
    from specklepy.api.client import SpeckleClient
    from specklepy.api.credentials import get_default_account
    from specklepy.transports.server import ServerTransport

    mesh = Mesh()
    smesh = SpeckleDataBridge.from_compas(mesh)

    client = SpeckleClient(host="speckle.xyz")
    account = get_default_account()
    client.authenticate(token=account.token)

    stream_id = 'ed4ebf6e29'
    transport = ServerTransport(client=client, stream_id=stream_id)
    object_id = operations.send(base=smesh, transports=[transport])
    commid_id = client.commit.create(stream_id=stream_id, object_id=object_id, message='Test commit')
```
