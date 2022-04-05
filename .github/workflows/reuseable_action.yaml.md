# A workflow that implement the "composite" action patter
name: Reuseable Composite Action
on: [push]

jobs:
  Print-inputs:
    runs-on: ubuntu-latest
    name: A job that print provided input
    steps:
      - uses: actions/checkout@v2
        id: Checkout
        name: Checkout action dir
      - uses: ./.github/actions/echoInput
        with:
          input-entered: "Hello from development"
        name: In dev
      - uses: ./.github/actions/echoInput
        with:
          input-entered: "Hello from staging"
        name: In stage
      - uses: ./.github/actions/echoInput
        with:
          input-entered: "Hello from production"
        name: In prod
      - uses: ./.github/actions/echoInput
        name: In default
      - run: echo the date is ${{ steps.Checkout.outputs.today-date }}
        shell: bash
        name: Show the date