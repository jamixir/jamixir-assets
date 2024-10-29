---
type: slide
theme: solarized

---
# JAM Meetup Lisbon
## Welcome

---

# Resources

## graypaper.com

---

# POAP
![Screenshot 2024-10-21 at 18.25.42](https://hackmd.io/_uploads/ByQjRW4gye.png =400x)
dotmemo.xyz/claim/jam-lisbon

---

# Teams 10min presentation

- Graymatter *(Oliver)*
- PyJAMaz *(Emiel)*
- Jamixir *(Daniel)*

---

## JAM Crypto Innovations

 - Polkadot Virtual Machine (PVM) - RISC-V
 - Erasure Coding DA
 - VRF Ring Signatures / Bandersnatch
 - In-core + on-chain 
 - Parallel Execution
     - Each Core runs different computing jobs
     - State components updated in parallel
 - Safrole and Grandpa - less forks

---

# Jamixir

---

# Why Elixir

 - Concurrency and Asynchronous I/O
 - Scalability and Fault Tolerancy
 - Ease of Implementation
 - Functional <=> Math Formal Spec
 - Developer Productivity 
 - Community and Ecosystem

---

## Block Structure
```Elixir
defmodule Block do
  @type t :: %__MODULE__{
    header: Block.Header.t(), 
    extrinsic: Block.Extrinsic.t()
  }

  defstruct [:header, :extrinsic]
end
```
![Screenshot 2024-10-21 at 17.50.28](https://hackmd.io/_uploads/r1mtIWElke.png =500x)

---

## Extrinsic Structure

```Elixir!
defmodule Block.Extrinsic do
  defstruct [:tickets, :disputes, :preimages, 
  :assurances, :guarantees]
end
```
![Screenshot 2024-10-21 at 17.50.28](https://hackmd.io/_uploads/r1mtIWElke.png =500x)

---

## State Structure

![Screenshot 2024-10-29 at 17.03.21](https://hackmd.io/_uploads/rJBFBcAlkx.png =700x)

```Elixir!
defmodule System.State do

  defstruct [
    :authorizer_pool,   # α
    :recent_history,    # β
    :safrole,           # γ
    :services,          # δ
    :entropy_pool,      # η
    ...
  ]
end
```

---


## State Transition Function
```Elixir
def add_block(%State{} = state, %Block{} = block) do
  # ...
end
```
![Screenshot 2024-10-22 at 19.38.10](https://hackmd.io/_uploads/BktE-OBe1x.png)

---


---

## State Merklization

![Screenshot 2024-10-21 at 18.01.12](https://hackmd.io/_uploads/rJGNK-ElJx.png)


```Elixir
  def merkelize_state(t) do
    merkelize(
      for {k, v} <- t do
        {bits(k), {k, v}}
      end
      |> Enum.into(%{})
    )
  end
```

