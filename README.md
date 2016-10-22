# weinberg-exp

export TOP=https://raw.githubusercontent.com/lukasheinrich/weinberg-exp/master/example_yadage
eval "$(curl https://raw.githubusercontent.com/diana-hep/yadage/master/yadagedocker.sh)"
yadage-run -t $TOP work_unpol rootflow.yml -p nevents=25000 -p seeds=[1,2,3,4] -a $TOP/input.zip -p runcardtempl=run_card.templ -p sqrtshalf=45 -p polbeam1=0 -p polbeam2=0 -p proccardtempl=sm_proc_card.templ



