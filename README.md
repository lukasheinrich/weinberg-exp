# weinberg-exp

[![yadage workflow](https://img.shields.io/badge/run_yadage-weinberg.yml-4187AD.svg)](http://yadage.cern.ch/submit?toplevel=github%3Alukasheinrich%2Fweinberg%3Aexample_yadage&workflow=rootflow.yml&pars=%7B%22sqrtshalf%22%3A+45%2C+%22Gf%22%3A+1.76639e-05%2C+%22nevents%22%3A+10000%2C+%22seeds%22%3A+%5B1%2C+2%2C+3%2C+4%5D%2C+%22polbeam1%22%3A+0%2C+%22polbeam2%22%3A+0%2C+%22paramcardtempl%22%3A+%22param_card.templ%22%2C+%22runcardtempl%22%3A+%22run_card.templ%22%2C+%22proccardtempl%22%3A+%22sm_proc_card.templ%22%7D&archive=https%3A%2F%2Fraw.githubusercontent.com%2Flukasheinrich%2Fweinberg-exp%2Fmaster%2Fexample_yadage%2Finput.zip&outputs=merge%2Fout.jsonl)

## Instructions:

this workflow generates a e+ e- > µ+ µ- events with polarized beams using madgraph and converts them to flat jsonlines files. If you cannot install `yadage` you can use the Docker image as shown below (This needs Docker installed, see documentation here: https://docs.docker.com/)

    export TOP=https://raw.githubusercontent.com/lukasheinrich/weinberg-exp/master/example_yadage
    eval "$(curl https://raw.githubusercontent.com/diana-hep/yadage/master/yadagedocker.sh)"
    yadage-run -t $TOP workdir_actmod rootflow.yml -p nevents=10000 -p seeds=[1,2,3,4] -a $TOP/input.zip \
	       -p runcardtempl=run_card.templ -p proccardtempl=sm_proc_card.templ \
               -p sqrtshalf=45 -p polbeam1=0 -p polbeam2=0 \
               -p Gf=1.766390e-05 -p paramcardtempl=param_card.templ


With yadage installed (`pip install yadage`) you can skip the `eval` line.

## Options

Polarization: `polbeam1` and `polbeam2` control the beam polarizations and can be varies from -100 to 100 each.

`nevents`: number of events to generate per seed
`seeds`: Array of seeds for random number generation

The number of events generated will be `(nevents) x len(seeds)`, i.e. in the examples above 100k events will be generated along four parallel production chains (each with a different seed)

## Example Output

The resulting file will be in `{workdir}/merge/out.jsonl`. Below we show a single event to illustrate the resulting JSON structure

        {
      "particles": [
        {
          "status": -1,
          "e": 45,
          "mother1": 0,
          "mother2": 0,
          "pz": 45,
          "px": 0,
          "py": 0,
          "m": 0,
          "color1": 0,
          "color2": 0,
          "lifetime": 0,
          "spin": 1,
          "id": -11
        },
        {
          "status": -1,
          "e": 45,
          "mother1": 0,
          "mother2": 0,
          "pz": -45,
          "px": -0,
          "py": -0,
          "m": 0,
          "color1": 0,
          "color2": 0,
          "lifetime": 0,
          "spin": -1,
          "id": 11
        },
        {
          "status": 2,
          "e": 90,
          "mother1": 1,
          "mother2": 2,
          "pz": 0,
          "px": 0,
          "py": 0,
          "m": 90,
          "color1": 0,
          "color2": 0,
          "lifetime": 0,
          "spin": 0,
          "id": 23
        },
        {
          "status": 1,
          "e": 45,
          "mother1": 3,
          "mother2": 3,
          "pz": -20.465267665,
          "px": -39.899107714,
          "py": 3.7728004224,
          "m": 0,
          "color1": 0,
          "color2": 0,
          "lifetime": 0,
          "spin": -1,
          "id": -13
        },
        {
          "status": 1,
          "e": 45,
          "mother1": 3,
          "mother2": 3,
          "pz": 20.465267665,
          "px": 39.899107714,
          "py": -3.7728004224,
          "m": 0,
          "color1": 0,
          "color2": 0,
          "lifetime": 0,
          "spin": 1,
          "id": 13
        }
      ],
      "eventinfo": {
        "scale": 90,
        "weight": 0.098172,
        "pid": 1,
        "nparticles": 5,
        "aqed": 0.007546771,
        "aqcd": 0.1182338
      }
    }

